```html id="ry7mhp"
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Hikma Travel Agency</title>

<meta name="description" content="Hikma Travel Agency provides education, scholarship, tourism and medical services in Türkiye.">
<meta name="keywords" content="Turkey scholarship, study in Turkey, medical tourism Turkey">
<meta name="author" content="Hikma Travel Agency">

<!-- React -->
<script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>

<!-- Babel -->
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

<!-- Tailwind -->
<script src="https://cdn.tailwindcss.com"></script>

<!-- Framer Motion -->
<script src="https://unpkg.com/framer-motion@10.16.4/dist/framer-motion.js"></script>

<!-- Icons -->
<script src="https://unpkg.com/@phosphor-icons/web"></script>

<!-- Marked -->
<script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>

<!-- Fonts -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700;900&family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">

<script>
tailwind.config = {
theme: {
extend: {
fontFamily: {
sans: ['Poppins', 'sans-serif'],
serif: ['Playfair Display', 'serif'],
},
colors: {
primary: '#12385f',
secondary: '#E86C15',
dark: '#111827',
light: '#f9fafb'
}
}
}
}
</script>

<style>

*{
margin:0;
padding:0;
box-sizing:border-box;
}

html{
scroll-behavior:smooth;
}

body{
font-family:'Poppins',sans-serif;
background:#f9fafb;
overflow-x:hidden;
}

h1,h2,h3,h4,h5,h6{
font-family:'Playfair Display',serif;
}

.glass-nav{
background:rgba(255,255,255,0.95);
backdrop-filter:blur(10px);
}

.hero-bg{
background-image:
linear-gradient(
to right,
rgba(18,56,95,0.9),
rgba(18,56,95,0.6)
),
url('https://images.unsplash.com/photo-1507525428034-b723cf961d3e?q=80&w=2070&auto=format&fit=crop');

background-size:cover;
background-position:center;
background-repeat:no-repeat;
}

::-webkit-scrollbar{
width:10px;
}

::-webkit-scrollbar-thumb{
background:#12385f;
border-radius:10px;
}

::-webkit-scrollbar-thumb:hover{
background:#E86C15;
}

.float-animation{
animation:floaty 4s ease-in-out infinite;
}

@keyframes floaty{
0%{
transform:translateY(0px);
}
50%{
transform:translateY(-10px);
}
100%{
transform:translateY(0px);
}
}

</style>
</head>

<body>

<div id="root"></div>

<script type="text/babel">

const { useState, useEffect } = React;
const { motion, AnimatePresence } = window.Motion;

const SectionHeading = ({title, subtitle}) => (
<div className="text-center mb-16">

<span className="text-secondary uppercase tracking-[0.2em] font-bold text-sm">
{subtitle}
</span>

<h2 className="text-4xl md:text-5xl font-bold text-primary mt-3">
{title}
</h2>

<div className="w-20 h-1 bg-secondary mx-auto rounded-full mt-5"></div>

</div>
);

const Navbar = () => {

const [scrolled, setScrolled] = useState(false);
const [mobileOpen, setMobileOpen] = useState(false);

useEffect(() => {

const handleScroll = () => {
setScrolled(window.scrollY > 50);
};

window.addEventListener('scroll', handleScroll);

return () => {
window.removeEventListener('scroll', handleScroll);
};

}, []);

useEffect(() => {

document.body.style.overflow = mobileOpen ? 'hidden' : 'auto';

return () => {
document.body.style.overflow = 'auto';
};

}, [mobileOpen]);

const links = [
{name:'Home', href:'#home'},
{name:'Services', href:'#services'},
{name:'Destinations', href:'#destinations'},
{name:'AI Planner', href:'#planner'},
{name:'Contact', href:'#contact'}
];

return(

<nav className={`fixed w-full z-50 transition-all duration-300 ${scrolled ? 'glass-nav py-3 shadow-md' : 'bg-transparent py-5'}`}>

<div className="container mx-auto px-6 flex justify-between items-center">

<a href="#home" className={`flex items-center ${scrolled ? 'text-primary' : 'text-white'}`}>

<div className="w-12 h-12 bg-white rounded-xl flex items-center justify-center relative">
<span className="text-primary text-3xl font-black">H</span>

<i className="ph-fill ph-airplane-tilt absolute -right-3 -top-2 text-secondary text-2xl -rotate-45"></i>
</div>

<div className="ml-4">
<h1 className="font-bold text-xl uppercase">
Hikma Travel
</h1>

<p className="uppercase tracking-[0.2em] text-xs text-secondary font-bold">
Agency
</p>
</div>

</a>

<div className="hidden md:flex items-center gap-8">

{links.map((link,index)=>(

<a
key={index}
href={link.href}
className={`${scrolled ? 'text-gray-800' : 'text-white'} hover:text-secondary transition`}
>
{link.name}
</a>

))}

<a
href="#contact"
className="bg-secondary text-white px-6 py-3 rounded-full font-bold hover:bg-orange-600 transition"
>
Book Now
</a>

</div>

<button
className={`md:hidden text-3xl ${scrolled ? 'text-primary' : 'text-white'}`}
onClick={() => setMobileOpen(!mobileOpen)}
>

<i className={`ph ${mobileOpen ? 'ph-x' : 'ph-list'}`}></i>

</button>

</div>

<AnimatePresence>

{mobileOpen && (

<motion.div
initial={{opacity:0,height:0}}
animate={{opacity:1,height:'auto'}}
exit={{opacity:0,height:0}}
className="bg-white md:hidden shadow-xl overflow-hidden"
>

<div className="p-6 flex flex-col gap-4">

{links.map((link,index)=>(

<a
key={index}
href={link.href}
onClick={() => setMobileOpen(false)}
className="border-b pb-3"
>
{link.name}
</a>

))}

</div>

</motion.div>

)}

</AnimatePresence>

</nav>

)
}

const Hero = () => (

<section id="home" className="hero-bg min-h-screen flex items-center justify-center text-center relative">

<div className="container mx-auto px-6">

<motion.p
initial={{opacity:0,y:30}}
animate={{opacity:1,y:0}}
className="text-secondary uppercase tracking-[0.2em] font-bold mb-6"
>
Premium Global Services
</motion.p>

<motion.h1
initial={{opacity:0,scale:0.9}}
animate={{opacity:1,scale:1}}
transition={{duration:0.7}}
className="text-5xl md:text-7xl font-bold text-white leading-tight"
>

Hikma Travel <br/>
Agency

</motion.h1>

<motion.p
initial={{opacity:0,y:20}}
animate={{opacity:1,y:0}}
transition={{delay:0.3}}
className="text-white/90 text-lg md:text-2xl mt-6 max-w-3xl mx-auto"
>

Your journey to education, scholarships,
tourism and healthcare in Türkiye starts here.

</motion.p>

<motion.div
initial={{opacity:0,y:20}}
animate={{opacity:1,y:0}}
transition={{delay:0.5}}
className="mt-10 flex flex-col sm:flex-row justify-center gap-4"
>

<a
href="#services"
className="bg-secondary text-white px-8 py-4 rounded-full font-bold hover:bg-orange-600 transition"
>
Explore Services
</a>

<a
href="#contact"
className="border-2 border-white text-white px-8 py-4 rounded-full font-bold hover:bg-white hover:text-primary transition"
>
Contact Us
</a>

</motion.div>

</div>

</section>

);

const Services = () => (

<section id="services" className="py-24 bg-white">

<div className="container mx-auto px-6">

<SectionHeading
title="Our Services"
subtitle="What We Offer"
/>

<div className="grid grid-cols-1 md:grid-cols-2 gap-10">

<div className="bg-gray-50 rounded-3xl overflow-hidden shadow-xl">

<div className="bg-primary p-8 text-white">

<h3 className="text-3xl font-bold">
Education Services
</h3>

<p className="mt-4 text-white/80">
Study opportunities in Türkiye.
</p>

</div>

<div className="p-8">

<ul className="space-y-4 text-gray-700">

<li>✅ University Admissions</li>
<li>✅ Student Visa Processing</li>
<li>✅ Scholarship Applications</li>
<li>✅ Accommodation Help</li>
<li>✅ Translation Services</li>

</ul>

</div>

</div>

<div className="bg-gray-50 rounded-3xl overflow-hidden shadow-xl">

<div className="bg-secondary p-8 text-white">

<h3 className="text-3xl font-bold">
Medical Tourism
</h3>

<p className="mt-4 text-white/90">
Professional healthcare support.
</p>

</div>

<div className="p-8">

<ul className="space-y-4 text-gray-700">

<li>✅ Hospital Appointments</li>
<li>✅ Medical Checkups</li>
<li>✅ Hotel Reservations</li>
<li>✅ Airport Transfers</li>
<li>✅ Tourism Packages</li>

</ul>

</div>

</div>

</div>

</div>

</section>

);

const Destinations = () => {

const destinations = [
{
title:'Student Life',
desc:'International student opportunities in Türkiye',
img:'https://images.unsplash.com/photo-1523050854058-8df90110c9f1?q=80&w=1000&auto=format&fit=crop'
},
{
title:'Medical Tourism',
desc:'Professional doctors and healthcare services',
img:'https://images.unsplash.com/photo-1584515933487-779824d29309?q=80&w=1000&auto=format&fit=crop'
},
{
title:'Türkiye Tours',
desc:'Explore beautiful destinations across Türkiye',
img:'https://images.unsplash.com/photo-1541432901042-2d8bd64b4a9b?q=80&w=1000&auto=format&fit=crop'
}
];

return(

<section id="destinations" className="py-24 bg-gray-50">

<div className="container mx-auto px-6">

<SectionHeading
title="Top Destinations"
subtitle="Explore Türkiye"
/>

<div className="grid grid-cols-1 md:grid-cols-3 gap-6">

{destinations.map((dest,index)=>(

<motion.div
key={index}
initial={{opacity:0,y:40}}
whileInView={{opacity:1,y:0}}
whileHover={{scale:1.03}}
transition={{duration:0.5,delay:index * 0.2}}
className="relative overflow-hidden rounded-3xl shadow-xl group"
>

<img
loading="lazy"
src={dest.img}
alt={dest.title}
className="w-full h-[420px] object-cover group-hover:scale-110 transition duration-700"
/>

<div className="absolute inset-0 bg-gradient-to-t from-black/80 via-black/20 to-transparent"></div>

<div className="absolute top-4 right-4 bg-white/20 backdrop-blur-md px-4 py-2 rounded-full text-white text-sm font-bold border border-white/20 float-animation">
✨ Hikma Travel
</div>

<div className="absolute bottom-0 p-6">

<h3 className="text-white text-3xl font-bold mb-2">
{dest.title}
</h3>

<p className="text-white/80">
{dest.desc}
</p>

</div>

</motion.div>

))}

</div>

</div>

</section>

)
}

const AIPlanner = () => {

const [prompt, setPrompt] = useState('');
const [loading, setLoading] = useState(false);
const [result, setResult] = useState('');

const generatePlan = async () => {

if(!prompt.trim()) return;

setLoading(true);

await new Promise(resolve => setTimeout(resolve, 2000));

const response = `
# Türkiye Travel Plan 🇹🇷

## Recommended Cities
- Istanbul
- Cappadocia
- Antalya

## Activities
- Historical Tours
- Medical Consultation
- Bosphorus Cruise
- Turkish Food Experience

## Duration
7 Days

Hikma Travel Agency can organize your entire journey professionally.
`;

setResult(marked.parse(response));

setLoading(false);
}

return(

<section id="planner" className="py-24 bg-white">

<div className="container mx-auto px-6">

<SectionHeading
title="AI Travel Planner"
subtitle="Smart Planning"
/>

<div className="max-w-4xl mx-auto bg-gray-50 rounded-3xl overflow-hidden shadow-xl">

<div className="bg-primary text-white p-8 text-center">

<h3 className="text-3xl font-bold">
Plan Your Dream Trip
</h3>

<p className="mt-4 text-white/80">
Ask our AI assistant anything about Türkiye.
</p>

</div>

<div className="p-8">

<div className="flex flex-col md:flex-row gap-4">

<input
type="text"
value={prompt}
onChange={(e)=>setPrompt(e.target.value)}
onKeyDown={(e)=>{
if(e.key==='Enter'){
generatePlan();
}
}}
placeholder="Example: Best 5-day tour in Istanbul"
className="flex-grow border border-gray-200 rounded-xl px-5 py-4 focus:outline-none focus:border-secondary"
/>

<button
onClick={generatePlan}
className="bg-secondary text-white px-8 py-4 rounded-xl font-bold hover:bg-orange-600 transition"
>

{loading ? (

<div className="flex items-center gap-3">

<div className="w-5 h-5 border-2 border-white border-t-transparent rounded-full animate-spin"></div>

<span>Generating...</span>

</div>

) : 'Generate'}

</button>

</div>

{result && (

<div
className="prose max-w-none mt-8 bg-white rounded-2xl p-8"
dangerouslySetInnerHTML={{__html:result}}
></div>

)}

</div>

</div>

</div>

</section>

)
}

const Footer = () => (

<footer id="contact" className="bg-dark text-white pt-20 pb-10">

<div className="container mx-auto px-6">

<div className="grid grid-cols-1 md:grid-cols-3 gap-12">

<div>

<h3 className="text-3xl font-bold mb-4">
Hikma Travel
</h3>

<p className="text-gray-400">
Your trusted partner for education and medical tourism in Türkiye.
</p>

</div>

<div>

<h4 className="text-xl font-bold mb-4">
Contact
</h4>

<ul className="space-y-3 text-gray-400">

<li>📍 Addis Ababa, Ethiopia</li>
<li>📞 +251 978 747 666</li>
<li>✉️ info@hikmatravel.com</li>

</ul>

</div>

<div>

<h4 className="text-xl font-bold mb-4">
Follow Us
</h4>

<div className="flex gap-4 text-2xl">

<a href="https://facebook.com" target="_blank">
<i className="ph-fill ph-facebook-logo"></i>
</a>

<a href="https://instagram.com" target="_blank">
<i className="ph-fill ph-instagram-logo"></i>
</a>

<a href="https://twitter.com" target="_blank">
<i className="ph-fill ph-twitter-logo"></i>
</a>

</div>

</div>

</div>

<div className="border-t border-white/10 mt-16 pt-8 text-center text-gray-500">
© 2026 Hikma Travel Agency. All rights reserved.
</div>

</div>

</footer>

)

const App = () => (
<div>

<Navbar />
<Hero />
<Services />
<Destinations />
<AIPlanner />
<Footer />

</div>
)

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);

</script>

</body>
</html>
```

