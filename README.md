# rakib-erp
erp
// frontend/src/OrderForm.jsx
import React, { useState } from 'react';
import axios from 'axios';

function OrderForm() {
  const [order, setOrder] = useState({
    order_no: '',
    buyer_name: '',
    style_no: '',
    quantity: '',
    order_date: '',
  });

  const handleChange = (e) => {
    setOrder({ ...order, [e.target.name]: e.target.value });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    axios.post('http://localhost:8000/api/orders/', order)
      .then(res => {
        alert('Order saved!');
        setOrder({ order_no: '', buyer_name: '', style_no: '', quantity: '', order_date: '' });
      })
      .catch(err => console.error(err));
  };

  return (
    <form onSubmit={handleSubmit}>
      <input name="order_no" placeholder="Order No" onChange={handleChange} value={order.order_no} />
      <input name="buyer_name" placeholder="Buyer Name" onChange={handleChange} value={order.buyer_name} />
      <input name="style_no" placeholder="Style No" onChange={handleChange} value={order.style_no} />
      <input name="quantity" placeholder="Quantity" type="number" onChange={handleChange} value={order.quantity} />
      <input name="order_date" placeholder="Order Date" type="date" onChange={handleChange} value={order.order_date} />
      <button type="submit">Save Order</button>
    </form>
  );
}

export default OrderForm;
