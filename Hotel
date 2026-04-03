import React, { useState, useEffect } from 'react';
import { 
  ShoppingBag, 
  X, 
  Plus, 
  Minus, 
  ChefHat, 
  MapPin, 
  Phone, 
  Clock, 
  Star,
  ChevronRight
} from 'lucide-react';

// --- CONFIGURATION ---
const OWNER_PHONE_NUMBER = "9100604776"; // Replace with your actual WhatsApp number with country code

// --- NON-VEG TIFFIN MENU DATA ---
const MENU_ITEMS = [
  {
    id: 1,
    name: "Mutton Paya with Idli",
    category: "Combos",
    price: 240,
    rating: 5.0,
    image: "https://images.unsplash.com/photo-1589301760014-d929f39ce9b1?auto=format&fit=crop&q=80&w=600",
    description: "Traditional slow-cooked goat trotter stew served with 3 soft, fluffy steamed idlis."
  },
  {
    id: 2,
    name: "Mutton Paya with Puri",
    category: "Combos",
    price: 250,
    rating: 4.9,
    image: "https://images.unsplash.com/photo-1627308595229-7830a5c91f9f?auto=format&fit=crop&q=80&w=600",
    description: "Rich, spicy Paya gravy served with 3 large, golden-fried fluffy wheat puris."
  },
  {
    id: 3,
    name: "Classic Egg Dosa",
    category: "Dosa",
    price: 110,
    rating: 4.7,
    image: "https://images.unsplash.com/photo-1668236543090-82eba5ee5976?auto=format&fit=crop&q=80&w=600",
    description: "Crispy dosa roasted with a cracked egg, pepper, and fresh coriander leaves."
  },
  {
    id: 4,
    name: "Non-Veg Podi Dosa",
    category: "Dosa",
    price: 130,
    rating: 4.8,
    image: "https://images.unsplash.com/photo-1630313224021-d607b66d6092?auto=format&fit=crop&q=80&w=600",
    description: "Spicy gunpowder (Podi) dosa layered with ghee and subtle hints of dried prawn powder."
  },
  {
    id: 5,
    name: "Mutton Keema Dosa",
    category: "Dosa",
    price: 190,
    rating: 4.9,
    image: "https://images.unsplash.com/photo-1645177628172-a94c1f96e6db?auto=format&fit=crop&q=80&w=600",
    description: "Our bestseller: Dosa stuffed with juicy, spiced minced mutton masala."
  },
  {
    id: 6,
    name: "Chicken Kari Dosa",
    category: "Dosa",
    price: 160,
    rating: 4.8,
    image: "https://images.unsplash.com/photo-1625398407796-82650a8c135f?auto=format&fit=crop&q=80&w=600",
    description: "Thick Madurai-style dosa topped with shredded chicken curry and spices."
  },
  {
    id: 7,
    name: "Egg Appam (2 pcs)",
    category: "Appam",
    price: 120,
    rating: 4.7,
    image: "https://images.unsplash.com/photo-1599487488170-d11ec9c172f0?auto=format&fit=crop&q=80&w=600",
    description: "Soft centered lacy pancakes with a whole egg cooked right in the middle."
  },
  {
    id: 8,
    name: "Chicken Liver Pepper Fry",
    category: "Sides",
    price: 140,
    rating: 4.6,
    image: "https://images.unsplash.com/photo-1601050690597-df056fb4ce99?auto=format&fit=crop&q=80&w=600",
    description: "Dry roasted chicken liver with heavy black pepper and curry leaves."
  }
];

const CATEGORIES = ["All", "Dosa", "Appam", "Combos", "Sides"];

export default function App() {
  const [cart, setCart] = useState([]);
  const [isCartOpen, setIsCartOpen] = useState(false);
  const [activeCategory, setActiveCategory] = useState("All");
  const [showNotification, setShowNotification] = useState(false);
  const [notificationMsg, setNotificationMsg] = useState("");

  const filteredItems = activeCategory === "All" 
    ? MENU_ITEMS 
    : MENU_ITEMS.filter(item => item.category === activeCategory);

  const addToCart = (item) => {
    setCart(prevCart => {
      const existingItem = prevCart.find(cartItem => cartItem.id === item.id);
      if (existingItem) {
        return prevCart.map(cartItem => 
          cartItem.id === item.id 
            ? { ...cartItem, quantity: cartItem.quantity + 1 } 
            : cartItem
        );
      }
      return [...prevCart, { ...item, quantity: 1 }];
    });
    
    setNotificationMsg(`Added ${item.name} to cart`);
    setShowNotification(true);
    setTimeout(() => setShowNotification(false), 2000);
  };

  const updateQuantity = (id, delta) => {
    setCart(prevCart => {
      return prevCart.map(item => {
        if (item.id === id) {
          const newQuantity = item.quantity + delta;
          return newQuantity > 0 ? { ...item, quantity: newQuantity } : item;
        }
        return item;
      });
    });
  };

  const removeFromCart = (id) => {
    setCart(prevCart => prevCart.filter(item => item.id !== id));
  };

  const cartTotal = cart.reduce((total, item) => total + (item.price * item.quantity), 0);
  const cartItemsCount = cart.reduce((count, item) => count + item.quantity, 0);

  const scrollToMenu = () => {
    document.getElementById('menu-section')?.scrollIntoView({ behavior: 'smooth' });
  };

  const handleCheckout = () => {
    if (cart.length === 0) return;

    let message = `*New Order from Non-Veg Tiffin Express*\n`;
    message += `----------------------------\n`;
    
    cart.forEach((item, index) => {
      message += `${index + 1}. ${item.name} x ${item.quantity} = ₹${item.price * item.quantity}\n`;
    });

    message += `----------------------------\n`;
    message += `*Total Amount: ₹${cartTotal}*\n\n`;
    message += `Please confirm my order. Thank you!`;

    const encodedMessage = encodeURIComponent(message);
    const whatsappUrl = `https://wa.me/${OWNER_PHONE_NUMBER}?text=${encodedMessage}`;
    
    window.open(whatsappUrl, '_blank');
  };

  return (
    <div className="min-h-screen bg-neutral-50 font-sans text-neutral-800">
      
      {/* --- NOTIFICATION TOAST --- */}
      <div className={`fixed top-24 left-1/2 transform -translate-x-1/2 z-50 transition-all duration-300 ${showNotification ? 'opacity-100 translate-y-0' : 'opacity-0 -translate-y-4 pointer-events-none'}`}>
        <div className="bg-red-600 text-white px-6 py-3 rounded-full shadow-lg font-medium text-sm flex items-center gap-2">
          <ChefHat size={16} />
          {notificationMsg}
        </div>
      </div>

      {/* --- HEADER --- */}
      <header className="sticky top-0 w-full bg-white shadow-sm z-40 border-b border-red-100">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
          <div className="flex items-center gap-2 text-red-600">
            <ChefHat size={32} strokeWidth={2.5} />
            <div className="flex flex-col">
              <h1 className="text-xl font-black tracking-tight uppercase leading-none">Non-Veg</h1>
              <span className="text-neutral-800 text-sm font-bold uppercase tracking-widest">Tiffin Express</span>
            </div>
          </div>
          
          <nav className="hidden md:flex items-center gap-8 font-semibold text-neutral-600">
            <a href="#home" className="hover:text-red-600 transition-colors">Home</a>
            <a href="#menu-section" className="hover:text-red-600 transition-colors">Menu</a>
            <a href="#about" className="hover:text-red-600 transition-colors">About</a>
          </nav>

          <button 
            onClick={() => setIsCartOpen(true)}
            className="relative p-3 text-neutral-700 hover:text-red-600 transition-colors bg-red-50 rounded-full"
          >
            <ShoppingBag size={24} />
            {cartItemsCount > 0 && (
              <span className="absolute -top-1 -right-1 bg-red-600 text-white text-xs font-bold w-6 h-6 flex items-center justify-center rounded-full border-2 border-white">
                {cartItemsCount}
              </span>
            )}
          </button>
        </div>
      </header>

      {/* --- HERO SECTION --- */}
      <section id="home" className="relative h-[60vh] flex items-center justify-center overflow-hidden">
        <div className="absolute inset-0">
          <img 
            src="https://images.unsplash.com/photo-1544148103-0773bf10d330?auto=format&fit=crop&q=80&w=2000" 
            alt="Spicy South Indian Food" 
            className="w-full h-full object-cover"
          />
          <div className="absolute inset-0 bg-gradient-to-t from-neutral-900 via-neutral-900/60 to-transparent"></div>
        </div>
        
        <div className="relative z-10 text-center px-4 max-w-4xl mx-auto mt-20">
          <span className="inline-block py-1 px-4 rounded-full bg-red-600 text-white font-bold tracking-wider text-xs mb-6 uppercase shadow-lg">
            Best Non-Veg Tiffins in Town
          </span>
          <h2 className="text-4xl md:text-6xl font-black text-white mb-6 leading-tight">
            Authentic Paya & Kari Dosa <br /> <span className="text-red-500">Delivered Hot.</span>
          </h2>
          <button 
            onClick={scrollToMenu}
            className="bg-white text-neutral-900 hover:bg-red-600 hover:text-white px-10 py-4 rounded-full font-black text-lg transition-all hover:scale-105 shadow-xl flex items-center gap-2 mx-auto"
          >
            Explore Menu <ChevronRight size={20} />
          </button>
        </div>
      </section>

      {/* --- MENU SECTION --- */}
      <section id="menu-section" className="py-16 bg-white">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          
          <div className="flex flex-col md:flex-row md:items-end justify-between mb-10 gap-6">
            <div>
              <h3 className="text-3xl font-black text-neutral-900 uppercase">The Tiffin Menu</h3>
              <p className="text-neutral-500 font-medium">Freshly prepared non-vegetarian specialties</p>
            </div>
            
            <div className="flex flex-wrap gap-2">
              {CATEGORIES.map(category => (
                <button
                  key={category}
                  onClick={() => setActiveCategory(category)}
                  className={`px-5 py-2 rounded-xl font-bold text-sm transition-all ${
                    activeCategory === category 
                      ? 'bg-red-600 text-white shadow-lg shadow-red-200' 
                      : 'bg-neutral-100 text-neutral-600 hover:bg-neutral-200'
                  }`}
                >
                  {category}
                </button>
              ))}
            </div>
          </div>

          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
            {filteredItems.map(item => (
              <div key={item.id} className="bg-white rounded-3xl overflow-hidden border border-neutral-100 shadow-sm hover:shadow-xl transition-all duration-300 flex flex-col">
                <div className="relative h-48 overflow-hidden">
                  <img 
                    src={item.image} 
                    alt={item.name} 
                    className="w-full h-full object-cover transition-transform duration-700 hover:scale-110"
                  />
                  <div className="absolute top-3 left-3 bg-white/90 backdrop-blur px-2 py-1 rounded-lg text-xs font-bold flex items-center gap-1 shadow-sm">
                    <Star size={12} className="text-yellow-500 fill-yellow-500" /> {item.rating}
                  </div>
                </div>
                <div className="p-5 flex flex-col flex-1">
                  <div className="flex justify-between items-start mb-2">
                    <h4 className="text-lg font-black text-neutral-900 leading-tight">{item.name}</h4>
                    <span className="text-red-600 font-black">₹{item.price}</span>
                  </div>
                  <p className="text-neutral-500 text-xs mb-6 line-clamp-2">{item.description}</p>
                  
                  <button 
                    onClick={() => addToCart(item)}
                    className="mt-auto w-full bg-neutral-900 hover:bg-red-600 text-white py-3 rounded-2xl font-bold transition-all flex items-center justify-center gap-2 group"
                  >
                    <Plus size={18} className="group-hover:rotate-90 transition-transform" /> Add
                  </button>
                </div>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* --- INFO SECTION --- */}
      <section id="about" className="py-16 bg-neutral-100">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
            <div className="bg-white p-8 rounded-3xl shadow-sm flex items-start gap-5">
              <div className="p-3 bg-red-50 text-red-600 rounded-2xl"><Clock size={28}/></div>
              <div>
                <h5 className="font-black text-neutral-900 mb-1">Service Hours</h5>
                <p className="text-sm text-neutral-500">7:00 AM - 11:30 AM</p>
                <p className="text-sm text-neutral-500">5:30 PM - 10:00 PM</p>
              </div>
            </div>
            <div className="bg-white p-8 rounded-3xl shadow-sm flex items-start gap-5">
              <div className="p-3 bg-red-50 text-red-600 rounded-2xl"><MapPin size={28}/></div>
              <div>
                <h5 className="font-black text-neutral-900 mb-1">Our Spot</h5>
                <p className="text-sm text-neutral-500">Shop No 42, Paya Street</p>
                <p className="text-sm text-neutral-500">Tiffin Nagar, TN 50002</p>
              </div>
            </div>
            <div className="bg-white p-8 rounded-3xl shadow-sm flex items-start gap-5">
              <div className="p-3 bg-red-50 text-red-600 rounded-2xl"><Phone size={28}/></div>
              <div>
                <h5 className="font-black text-neutral-900 mb-1">Quick Delivery</h5>
                <p className="text-sm text-neutral-500">{OWNER_PHONE_NUMBER}</p>
                <p className="text-sm text-neutral-500">Delivery in 20 mins</p>
              </div>
            </div>
          </div>
        </div>
      </section>

      <footer className="bg-white py-10 text-center border-t border-neutral-100">
        <div className="flex items-center justify-center gap-2 text-red-600 mb-4">
          <ChefHat size={24} />
          <span className="font-black uppercase tracking-tighter">Non-Veg Tiffin Express</span>
        </div>
        <p className="text-neutral-400 text-xs uppercase tracking-widest font-bold">Stay Spicy &bull; Eat Fresh &bull; © 2026</p>
      </footer>

      {/* --- CART DRAWER --- */}
      {isCartOpen && (
        <div className="fixed inset-0 z-50 flex justify-end">
          <div className="absolute inset-0 bg-black/40 backdrop-blur-sm transition-opacity" onClick={() => setIsCartOpen(false)}></div>
          <div className="relative w-full max-w-md bg-white h-full shadow-2xl flex flex-col">
            <div className="p-6 border-b flex items-center justify-between">
              <div className="flex items-center gap-3">
                <ShoppingBag size={24} className="text-red-600" />
                <h2 className="text-xl font-black">Your Order</h2>
              </div>
              <button onClick={() => setIsCartOpen(false)} className="p-2 hover:bg-neutral-100 rounded-full"><X size={24} /></button>
            </div>

            <div className="flex-1 overflow-y-auto p-6">
              {cart.length === 0 ? (
                <div className="h-full flex flex-col items-center justify-center text-neutral-400 space-y-3">
                  <ChefHat size={48} className="opacity-20" />
                  <p className="font-bold">Cart is empty</p>
                </div>
              ) : (
                <div className="space-y-4">
                  {cart.map(item => (
                    <div key={item.id} className="flex gap-4 items-center bg-neutral-50 p-4 rounded-2xl">
                      <img src={item.image} alt={item.name} className="w-16 h-16 object-cover rounded-xl" />
                      <div className="flex-1">
                        <h4 className="font-bold text-sm">{item.name}</h4>
                        <div className="text-red-600 font-black text-xs">₹{item.price}</div>
                        <div className="flex items-center gap-3 mt-2">
                          <button onClick={() => updateQuantity(item.id, -1)} className="w-6 h-6 flex items-center justify-center rounded bg-white border border-neutral-200"><Minus size={12}/></button>
                          <span className="text-sm font-bold">{item.quantity}</span>
                          <button onClick={() => updateQuantity(item.id, 1)} className="w-6 h-6 flex items-center justify-center rounded bg-white border border-neutral-200"><Plus size={12}/></button>
                        </div>
                      </div>
                      <button onClick={() => removeFromCart(item.id)} className="text-neutral-300 hover:text-red-600"><X size={20}/></button>
                    </div>
                  ))}
                </div>
              )}
            </div>

            {cart.length > 0 && (
              <div className="p-6 bg-neutral-50 border-t">
                <div className="flex justify-between font-black text-2xl mb-6">
                  <span>Total</span>
                  <span className="text-red-600">₹{cartTotal}</span>
                </div>
                <button 
                  onClick={handleCheckout}
                  className="w-full bg-green-600 hover:bg-green-700 text-white py-4 rounded-2xl font-black text-lg shadow-lg shadow-green-100 active:scale-95 transition-all flex items-center justify-center gap-2"
                >
                  Checkout via WhatsApp
                </button>
                <p className="text-center text-[10px] text-neutral-400 mt-3 font-bold uppercase tracking-widest">Order will be sent to owner via WhatsApp</p>
              </div>
            )}
          </div>
        </div>
      )}
    </div>
  );
}
