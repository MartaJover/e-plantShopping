this is  ProductList.jsx:
```javascript
import React, { useState,useEffect } from 'react';
import './ProductList.css'
import CartItem from './CartItem';
import { addItem, updateQuantity } from './CartSlice';
import { useDispatch, useSelector } from 'react-redux';

function ProductList() {
    const [showCart, setShowCart] = useState(false); 
    const [showPlants, setShowPlants] = useState(false); // State to control the visibility of the About Us page
    const dispatch = useDispatch();
    const cart = useSelector(state => state.cart.items);
    const [addedToCart, setAddedToCart] = useState({});

    const plantsArray = [
        {
            category: "Air Purifying Plants",
            plants: [
                {
                    name: "Snake Plant",
                    image: "https://cdn.pixabay.com/photo/2021/01/22/06/04/snake-plant-5939187_1280.jpg",
                    description: "Produces oxygen at night, improving air quality.",
                    cost: "$15"
                },
                {
                    name: "Spider Plant",
                    image: "https://cdn.pixabay.com/photo/2018/07/11/06/47/chlorophytum-3530413_1280.jpg",
                    description: "Filters formaldehyde and xylene from the air.",
                    cost: "$12"
                },
                {
                    name: "Peace Lily",
                    image: "https://cdn.pixabay.com/photo/2019/06/12/14/14/peace-lilies-4269365_1280.jpg",
                    description: "Removes mold spores and purifies the air.",
                    cost: "$18"
                },
                {
                    name: "Boston Fern",
                    image: "https://cdn.pixabay.com/photo/2020/04/30/19/52/boston-fern-5114414_1280.jpg",
                    description: "Adds humidity to the air and removes toxins.",
                    cost: "$20"
                },
                {
                    name: "Rubber Plant",
                    image: "https://cdn.pixabay.com/photo/2020/02/15/11/49/flower-4850729_1280.jpg",
                    description: "Easy to care for and effective at removing toxins.",
                    cost: "$17"
                },
                {
                    name: "Aloe Vera",
                    image: "https://cdn.pixabay.com/photo/2018/04/02/07/42/leaf-3283175_1280.jpg",
                    description: "Purifies the air and has healing properties for skin.",
                    cost: "$14"
                }
            ]
        },
        {
            category: "Aromatic Fragrant Plants",
            plants: [
                {
                    name: "Lavender",
                    image: "https://images.unsplash.com/photo-1611909023032-2d6b3134ecba?q=80&w=1074&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
                    description: "Calming scent, used in aromatherapy.",
                    cost: "$20"
                },
                {
                    name: "Jasmine",
                    image: "https://images.unsplash.com/photo-1592729645009-b96d1e63d14b?q=80&w=1170&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
                    description: "Sweet fragrance, promotes relaxation.",
                    cost: "$18"
                },
                {
                    name: "Rosemary",
                    image: "https://cdn.pixabay.com/photo/2019/10/11/07/12/rosemary-4541241_1280.jpg",
                    description: "Invigorating scent, often used in cooking.",
                    cost: "$15"
                },
                {
                    name: "Mint",
                    image: "https://cdn.pixabay.com/photo/2016/01/07/18/16/mint-1126282_1280.jpg",
                    description: "Refreshing aroma, used in teas and cooking.",
                    cost: "$12"
                },
                {
                    name: "Lemon Balm",
                    image: "https://cdn.pixabay.com/photo/2019/09/16/07/41/balm-4480134_1280.jpg",
                    description: "Citrusy scent, relieves stress and promotes sleep.",
                    cost: "$14"
                },
                {
                    name: "Hyacinth",
                    image: "https://cdn.pixabay.com/photo/2019/04/07/20/20/hyacinth-4110726_1280.jpg",
                    description: "Hyacinth is a beautiful flowering plant known for its fragrant.",
                    cost: "$22"
                }
            ]
        },
        {
            category: "Insect Repellent Plants",
            plants: [
                {
                    name: "oregano",
                    image: "https://cdn.pixabay.com/photo/2015/05/30/21/20/oregano-790702_1280.jpg",
                    description: "The oregano plants contains compounds that can deter certain insects.",
                    cost: "$10"
                },
                {
                    name: "Marigold",
                    image:"https://cdn.pixabay.com/photo/2022/02/22/05/45/marigold-7028063_1280.jpg",
                    description: "Natural insect repellent, also adds color to the garden.",
                    cost: "$8"
                },
                {
                    name: "Geraniums",
                    image: "https://cdn.pixabay.com/photo/2012/04/26/21/51/flowerpot-43270_1280.jpg",
                    description: "Known for their insect-repelling properties while adding a pleasant scent.",
                    cost: "$20"
                },
                {
                    name: "Basil",
                    image: "https://cdn.pixabay.com/photo/2016/07/24/20/48/tulsi-1539181_1280.jpg",
                    description: "Repels flies and mosquitoes, also used in cooking.",
                    cost: "$9"
                },
                {
                    name: "Lavender",
                    image: "https://images.unsplash.com/photo-1611909023032-2d6b3134ecba?q=80&w=1074&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
                    description: "Calming scent, used in aromatherapy.",
                    cost: "$20"
                },
                {
                    name: "Catnip",
                    image: "https://cdn.pixabay.com/photo/2015/07/02/21/55/cat-829681_1280.jpg",
                    description: "Repels mosquitoes and attracts cats.",
                    cost: "$13"
                }
            ]
        },
        {
            category: "Medicinal Plants",
            plants: [
                {
                    name: "Aloe Vera",
                    image: "https://cdn.pixabay.com/photo/2018/04/02/07/42/leaf-3283175_1280.jpg",
                    description: "Soothing gel used for skin ailments.",
                    cost: "$14"
                },
                {
                    name: "Echinacea",
                    image: "https://cdn.pixabay.com/photo/2014/12/05/03/53/echinacea-557477_1280.jpg",
                    description: "Boosts immune system, helps fight colds.",
                    cost: "$16"
                },
                {
                    name: "Peppermint",
                    image: "https://cdn.pixabay.com/photo/2017/07/12/12/23/peppermint-2496773_1280.jpg",
                    description: "Relieves digestive issues and headaches.",
                    cost: "$13"
                },
                {
                    name: "Lemon Balm",
                    image: "https://cdn.pixabay.com/photo/2019/09/16/07/41/balm-4480134_1280.jpg",
                    description: "Calms nerves and promotes relaxation.",
                    cost: "$14"
                },
                {
                    name: "Chamomile",
                    image: "https://cdn.pixabay.com/photo/2016/08/19/19/48/flowers-1606041_1280.jpg",
                    description: "Soothes anxiety and promotes sleep.",
                    cost: "$15"
                },
                {
                    name: "Calendula",
                    image: "https://cdn.pixabay.com/photo/2019/07/15/18/28/flowers-4340127_1280.jpg",
                    description: "Heals wounds and soothes skin irritations.",
                    cost: "$12"
                }
            ]
        },
        {
            category: "Low Maintenance Plants",
            plants: [
                {
                    name: "ZZ Plant",
                    image: "https://images.unsplash.com/photo-1632207691143-643e2a9a9361?q=80&w=464&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
                    description: "Thrives in low light and requires minimal watering.",
                    cost: "$25"
                },
                {
                    name: "Pothos",
                    image: "https://cdn.pixabay.com/photo/2018/11/15/10/32/plants-3816945_1280.jpg",
                    description: "Tolerates neglect and can grow in various conditions.",
                    cost: "$10"
                },
                {
                    name: "Snake Plant",
                    image: "https://cdn.pixabay.com/photo/2021/01/22/06/04/snake-plant-5939187_1280.jpg",
                    description: "Needs infrequent watering and is resilient to most pests.",
                    cost: "$15"
                },
                {
                    name: "Cast Iron Plant",
                    image: "https://cdn.pixabay.com/photo/2017/02/16/18/04/cast-iron-plant-2072008_1280.jpg",
                    description: "Hardy plant that tolerates low light and neglect.",
                    cost: "$20"
                },
                {
                    name: "Succulents",
                    image: "https://cdn.pixabay.com/photo/2016/11/21/16/05/cacti-1846147_1280.jpg",
                    description: "Drought-tolerant plants with unique shapes and colors.",
                    cost: "$18"
                },
                {
                    name: "Aglaonema",
                    image: "https://cdn.pixabay.com/photo/2014/10/10/04/27/aglaonema-482915_1280.jpg",
                    description: "Requires minimal care and adds color to indoor spaces.",
                    cost: "$22"
                }
            ]
        }
    ];

   const styleObj={
    backgroundColor: '#4CAF50',
    color: '#fff!important',
    padding: '15px',
    display: 'flex',
    justifyContent: 'space-between',
    alignIems: 'center',
    fontSize: '20px',
   }
   const styleObjUl={
    display: 'flex',
    justifyContent: 'space-between',
    alignItems: 'center',
    width: '1100px',
   }
   const styleA={
    color: 'white',
    fontSize: '30px',
    textDecoration: 'none',
   }
const handleCartClick = (e) => {
    e.preventDefault();
    setShowCart(true); // Set showCart to true when cart icon is clicked
    };
const handlePlantsClick = (e) => {
    e.preventDefault();
    setShowPlants(true); // Set showAboutUs to true when "About Us" link is clicked
    setShowCart(false); // Hide the cart when navigating to About Us
};

const handleContinueShopping = (e) => {
    e.preventDefault();
    setShowCart(false);
};

const handleAddToCart = (product) => {
    dispatch(addItem(product));
    setAddedToCart((prevState) => ({
       ...prevState,
       [product.name]: true, // Set the product name as key and value as true to indicate it's added to cart
     }));
  };

const Navbar = () => {
    const cart = useSelector(state => state.cart.items);
    // Calculate total quantity of all items in the cart
    const totalCartItems = cart.reduce((total, item) => total + item.quantity, 0);

        return (
            <div className="navbar">
                <h1>Paradise Nursery</h1>
                <div className="cart-icon">
                    🛒 <span className="cart-count">{totalCartItems}</span>
                </div>
            </div>
        );
};

    return (
        <div>
             <div className="navbar" style={styleObj}>
            <div className="tag">
               <div className="luxury">
                    <img src="https://cdn.pixabay.com/photo/2020/08/05/13/12/eco-5465432_1280.png" alt="" />
                    <a href="https://martajover.github.io/e-plantShopping/" style={{textDecoration:'none'}}>
                        <div>
                        <h3 style={{color:'white'}}>Paradise Nursery</h3>
                        <i style={{color:'white'}}>Where Green Meets Serenity</i>
                        </div>
                    </a>
                </div>
              
            </div>
            <div style={styleObjUl}>
                <div> <a href="#" onClick={(e) => handlePlantsClick(e)} style={styleA}>Plants</a></div>
                <div> <a href="#" onClick={(e) => handleCartClick(e)} style={styleA}>
                    <h1 className='cart'>
                    <span className="cart-count">
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 256 256" id="IconChangeColor" height="68" width="68">
                            <rect width="156" height="156" fill="none"></rect>
                            <circle cx="80" cy="216" r="12"></circle>
                            <circle cx="184" cy="216" r="12"></circle>
                            <path d="M42.3,72H221.7l-26.4,92.4A15.9,15.9,0,0,1,179.9,176H84.1a15.9,15.9,0,0,1-15.4-11.6L32.5,37.8A8,8,0,0,0,24.8,32H8" 
                                fill="none" stroke="#faf9f9" stroke-linecap="round" stroke-linejoin="round" stroke-width="2">
                            </path>
                        </svg>
                        <span className="cart-item-count">
                            {cart.reduce((total, item) => total + item.quantity, 0)}
                        </span>
                    </span>
                    </h1></a>
                </div>
            </div>
        </div>
        {!showCart? (
        <div className="product-grid">
        <h1>Plants</h1>
        {plantsArray.map((category, index) => (
            <div key={index}>
                <h2>{category.category}</h2>
                <div className="product-list">
                    {category.plants.map((plant, plantIndex) => {
                        // Check if item exists in cart to update button text
                        const isAdded = cart.some(item => item.name === plant.name);

                        return (
                            <div className="product-card" key={plantIndex}>
                                <img className="product-image" src={plant.image} alt={plant.name} />
                                <div className="product-title">{plant.name}</div>
                                <div className="product-cost">{plant.cost}</div>
                                <button
                                    className={`product-button ${isAdded ? "added-to-cart" : ""}`}
                                    onClick={() => handleAddToCart(plant)}
                                    disabled={isAdded} // Disable if already added
                                >
                                    {isAdded ? "Added to Cart" : "Add to Cart"}
                                </button>
                            </div>
                        );
                    })}
                </div>
            </div>
        ))}
    </div>
 ) :  (
    <CartItem onContinueShopping={handleContinueShopping}/>
)}
    </div>
    );
}

export default ProductList;


```

This is CartSlice.jsx:
```javascript
import { createSlice } from '@reduxjs/toolkit';

export const CartSlice = createSlice({
  name: 'cart',
  initialState: {
    items: [], // Initialize items as an empty array
  },
  reducers: {
    addItem: (state, action) => {
      const { name, image, cost } = action.payload;
      const existingItem = state.items.find(item => item.name === name);
      if (existingItem) {
        existingItem.quantity++;
      } else {
        state.items.push({ name, image, cost, quantity: 1 });
      }
    },
    removeItem: (state, action) => {
      state.items = state.items.filter(item => item.name !== action.payload);
    },
    updateQuantity: (state, action) => {
      const { name, quantity } = action.payload;
      const itemToUpdate = state.items.find(item => item.name === name);
      if (itemToUpdate) {
        itemToUpdate.quantity = quantity;
      }
    },
  },
});

export const { addItem, removeItem, updateQuantity } = CartSlice.actions;
export default CartSlice.reducer;
```

This is CartItem.jsx:
```javascript
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { removeItem, updateQuantity, addItem } from './CartSlice';
import './CartItem.css';

const CartItem = ({ onContinueShopping }) => {
  const cart = useSelector(state => state.cart.items);
  const dispatch = useDispatch();

  // Calculate total amount for all products in the cart
  const calculateTotalAmount = () => {
    let totalAmount = 0;
    cart.forEach((item) => {
      let price = parseFloat(item.cost.substring(1));
      totalAmount += price * item.quantity;
    });
    return totalAmount;
  };

  const handleContinueShopping = (e) => {
    onContinueShopping(e);
  };

  const handleIncrement = (item) => {
    dispatch(updateQuantity({name: item.name, quantity: item.quantity +1}));
  };

  const handleDecrement = (item) => {
    if (item.quantity > 1) {
    dispatch(updateQuantity({name: item.name, quantity: item.quantity -1}));
    } else {
      dispatch(removeItem(item.name));
    }
  };

  const handleRemove = (item) => {
    dispatch(removeItem(item.name));
  };

  // Calculate total cost based on quantity for an item
  const calculateTotalCost = (item) => {
    let totalCost = 0;
    let price = parseFloat(item.cost.substring(1));
    return price * item.quantity;
  };

  const handleCheckoutShopping = (e) => {
    alert('Functionality to be added for future reference');
  }

  return (
    <div className="cart-container">
      <h2 style={{ color: 'black' }}>Total Cart Amount: ${calculateTotalAmount()}</h2>
      <div>
        {cart.map(item => (
          <div className="cart-item" key={item.name}>
            <img className="cart-item-image" src={item.image} alt={item.name} />
            <div className="cart-item-details">
              <div className="cart-item-name">{item.name}</div>
              <div className="cart-item-cost">{item.cost}</div>
              <div className="cart-item-quantity">
                <button className="cart-item-button cart-item-button-dec" onClick={() => handleDecrement(item)}>-</button>
                <span className="cart-item-quantity-value">{item.quantity}</span>
                <button className="cart-item-button cart-item-button-inc" onClick={() => handleIncrement(item)}>+</button>
              </div>
              <div className="cart-item-total">Total: ${calculateTotalCost(item)}</div>
              <button className="cart-item-delete" onClick={() => handleRemove(item)}>Delete</button>
            </div>
          </div>
        ))}
      </div>
      <div style={{ marginTop: '20px', color: 'black' }} className='total_cart_amount'></div>
      <div className="continue_shopping_btn">
        <button className="get-started-button" onClick={(e) => handleContinueShopping(e)}>Continue Shopping</button>
        <br />
        <button className="get-started-button1">Checkout</button>
      </div>
    </div>
  );
};

export default CartItem;




```

This is ProductList.css:
```css
/* Reset some default styles */
body, h1, ul {
    margin: 0;
    padding: 0;
}

/* Set a background color */
body {
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
}

/* Navbar */
.navbar {
    background-color: #4CAF50;
    color: #fff!important;
    padding: 15px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 20px;
}

.navbar .ul {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 1100px;
}

.navbar li {
    margin-right: 30px;
}

.navbar .ul div a {
    color: white;
    font-size: 30px;
    text-decoration: none;
   
}

/* Product Grid */
.product-grid {
    display:flex;
    flex-direction: column;
    width: 100vw;
    align-items: center;
    justify-content: center;
}
.product-list {
    display: flex;
    flex-wrap: wrap;
    gap: 50px;
    /* background-color: pink; */
    /* justify-content: space-between; */
    padding: 20px;
    width: 100%;
    align-items: center;
    justify-content: center;
}

/* Product Card */
.product-card {
    flex: 0 0 calc(33.33% - 20px); /* Adjust width for 3 cards per row with 20px gap */
    max-width: calc(26.33% - 20px); /* Adjust max-width for 3 cards per row with 20px gap */
    margin-bottom: 20px;
    padding: 20px;
    background-color: #fff;
    border: 1px solid #ccc;
    border-radius: 5px;
    text-align: center;
    position: relative;
    
    gap: 20px;
}

/* Pseudo-classes - Hover effect on product button */
.product-card:hover {
    transform: scale(1.05);
    transition: transform 0.3s ease-in-out;
    z-index: 1;
}

.product-title {
    font-weight: bold;
    margin-bottom: 10px;
}

.product-price {
    color: #e74c3c;
    font-size: 1.2rem;
    margin-bottom: 10px;
}

.product-image {
    max-width: 100%;
    height: 200px; /* Adjust height for better consistency */
}

.product-button {
    background-color: #e74c3c;
    color: #fff;
    border: none;
    padding: 10px 20px;
    cursor: pointer;
    transition: background-color 0.3s ease-in-out;
    margin-top: 10px;
}

.product-button:hover {
    background-color: #c0392b;
}

/* When item is added to cart, change color */
.product-button.added-to-cart {
    background-color: grey;
    cursor: not-allowed;
}

/* Pseudo-elements - Sale badge */
.product-card::before {
    content: "SALE";
    background-color: #e74c3c;
    color: #fff;
    position: absolute;
    top: 0;
    right: 0;
    padding: 5px 10px;
    border-radius: 0 0 0 5px;
}
.tag_home_link{
    display: flex;
    /* background-color: red; */
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin-left: 50px;
    color: white;
    text-decoration: none;
    font-size: 20px;
}
.tag_home_link h3{
    font-size: 30px;
}
.tag a{
    text-decoration: none;
}
.tag {
    width: 400px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.tag img {
    height: 70px;
    width: 70px;
    border-radius: 70%;
    
}

.luxury {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 650px;
    font-size: 19px;
}
.cart{
    color: white;
    display: flex;
}
.cart_quantity_count{
    margin-top: 16px;
    /* background-color: red; */
    margin-left: 27px;
    position: absolute;
    font-size: 29px;

}
.plantname_heading{
   display: flex;
   align-items: center;
   justify-content: center;
    /* background-color: yellow; */
}
.plant_heading{
    width: 400px;
    text-align: center;
    margin: 20px;
    border: 1px solid rgb(5, 4, 4);
    border-left: none;
    border-right: none;

    
}
/* Add Media Query for responsiveness */
@media (max-width: 768px) {
    .product-card {
        flex: 1 1 calc(50% - 20px); /* Adjust width for 2 cards per row with 20px gap on smaller screens */
        max-width: calc(50% - 20px); /* Adjust max-width for 2 cards per row with 20px gap on smaller screens */
    }
}
/* ProductList.css */

.product-button {
    background-color: #4CAF50; /* Green */
    border: none;
    color: white;
    padding: 10px 20px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    transition-duration: 0.4s;
    cursor: pointer;
  }
  
  .product-button:hover {
    background-color: #45a049;
  }
  
  .product-button.added-to-cart {
    background-color: grey; /* Grey when product is added */
  }
  @media (max-width: 1200px) {
    .product-card {
      flex: 1 1 calc(33.33% - 20px); /* Adjust width for 3 cards per row with 20px gap on medium screens */
      max-width: calc(33.33% - 20px); /* Adjust max-width for 3 cards per row with 20px gap on medium screens */
    }
  }
  
  @media (max-width: 768px) {
    .product-card {
      flex: 1 1 calc(50% - 20px); /* Adjust width for 2 cards per row with 20px gap on small screens */
      max-width: calc(50% - 20px); /* Adjust max-width for 2 cards per row with 20px gap on small screens */
    }
    .navbar {
        flex-direction: column; /* Change flex direction to stack items vertically */
        align-items: center; /* Align items to the center of the container */
      }
    
      .tag {
        margin-bottom: 20px; /* Add margin bottom for spacing */
        text-align: center; /* Align text to the center */
      }
    
      .ul {
        display: flex; /* Set display to flex */
        flex-direction: column; /* Change flex direction to stack items vertically */
        gap: 10px; /* Add gap between items */
      }
    
      .ul div {
        text-align: center; /* Align text to the center */
      }
  }
```

I have a problem somewhere and I don't know where. 
After adding something to the cart (pressing the button called product-button), the cart icon doesn't show any number.
Also, the "Add to cart" button (product-button) from the product cards does not change to "Added to cart". 
However, if I click "add to cart" button (product-button) several times, the item appears in the cart with as much quantity as the times I clicked the button.
This means that the bsckend behaviour is correct, but not the front visualisation

I want the front to make a 'onClick' change once i press the product-button
I want you to make this edit for me and eli5