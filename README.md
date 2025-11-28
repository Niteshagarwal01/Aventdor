# 🚗 Aventador — Luxury Car Portfolio (Small Build \#7)

\<p align="center"\>
\<img src="assets/img/home-car-1.png" alt="Aventador Hero Image" width="100%" /\>
\</p\>

A premium, fully responsive automotive landing page designed to showcase luxury vehicles with immersive animations and smooth interactions. Built with semantic HTML, modern CSS, and JavaScript libraries to deliver a high-end user experience.

## 🚀 Features

  * **Immersive Hero Section:** Full-screen layout with 3D-style car presentation and call-to-action.
  * **Touch-Responsive Sliders:** Powered by Swiper.js for seamless browsing of car models on mobile and desktop.
  * **Scroll Reveal Animations:** Elements cascade into view as the user scrolls, creating a dynamic narrative flow.
  * **Glassmorphism UI:** Modern translucent card effects and blurred backgrounds for a premium aesthetic.
  * **Sticky Navigation:** Smart header that changes appearance on scroll with active section highlighting.
  * **Brand Philosophy Section:** Elegant typography and layout to tell the brand's story.
  * **Responsive Grid:** Fluid layouts that adapt perfectly from 320px mobile screens to 4K desktops.
  * **Interactive Features:** Hover effects on buttons, cards, and specifications for better engagement.
  * **Performance Optimized:** Minimized render-blocking resources for high Lighthouse scores.
  * **Modular CSS:** Uses CSS Variables for easy theming and consistent spacing.

## 🛠️ Tech Stack

  * **Structure:** HTML5 (Semantic BEM naming convention)
  * **Styling:** CSS3 (Flexbox, Grid, Custom Properties, Media Queries)
  * **Logic:** Vanilla JavaScript (ES6+)
  * **Libraries:**
      * **Swiper.js:** For touch-enabled, hardware-accelerated carousels.
      * **ScrollReveal.js:** For sequencing entrance animations.
      * **Remix Icons:** For lightweight, vector-based interface icons.

## 📂 File Structure

  * `index.html` - The main structure containing Hero, About, Popular, and Features sections.
  * `assets/css/styles.css` - comprehensive styling with root variables for colors and fonts.
  * `assets/js/main.js` - Handles DOM manipulation, library initialization, and scroll logic.
  * `assets/img/` - Optimized assets for car models and logos.

## ⚙️ How It Works

The application relies on `main.js` to handle UI state changes and initialize third-party libraries.

### 1\. Swiper.js Configuration

We use two distinct Swiper instances. The "Popular" section uses a centered-slide layout with grab-cursor enabled.

```javascript
let swiperPopular = new Swiper(".popular__container", {
  loop: true,
  spaceBetween: 24,
  slidesPerView: "auto",
  grabCursor: true,
  pagination: {
    el: ".swiper-pagination",
    dynamicBullets: true,
  },
  breakpoints: {
    768: {
      slidesPerView: 3, // Shows 3 cars on tablet/desktop
    },
    1024: {
      spaceBetween: 48,
    },
  },
});
```

### 2\. ScrollReveal Animation Logic

Instead of standard CSS transitions, we use ScrollReveal to orchestrate complex entrance sequences without cluttering the CSS.

```javascript
const sr = ScrollReveal({
  origin: 'top',
  distance: '60px',
  duration: 2500,
  delay: 400,
  // reset: true // Animation repeats on scroll up
});

// Staggered animations for different elements
sr.reveal(`.home__title, .popular__container, .features__img, .featured__filters`);
sr.reveal(`.home__subtitle`, { delay: 500 });
sr.reveal(`.home__elec`, { delay: 600 });
sr.reveal(`.home__img`, { delay: 800 });
sr.reveal(`.home__car-data`, { delay: 900, interval: 100, origin: 'bottom' });
```

### 3\. Active Scroll Spy

The navigation menu automatically updates to reflect the current section in the viewport using `scrollY` and element offsets.

```javascript
const sections = document.querySelectorAll('section[id]')

function scrollActive(){
    const scrollY = window.pageYOffset

    sections.forEach(current =>{
        const sectionHeight = current.offsetHeight,
              sectionTop = current.offsetTop - 58,
              sectionId = current.getAttribute('id')

        if(scrollY > sectionTop && scrollY <= sectionTop + sectionHeight){
            document.querySelector('.nav__menu a[href*=' + sectionId + ']').classList.add('active-link')
        }else{
            document.querySelector('.nav__menu a[href*=' + sectionId + ']').classList.remove('active-link')
        }
    })
}
window.addEventListener('scroll', scrollActive)
```

## 💻 Run Locally

1.  Clone the repository:
    ```bash
    git clone https://github.com/Niteshagarwal01/aventdor.git
    cd aventdor
    ```
2.  Open `index.html` in your browser.
3.  **No Node.js/NPM required:** This is a static site build. All libraries are included via CDN or local assets.

## 🔧 Customization

  * **Color Theme:** Modify the CSS variables in `assets/css/styles.css` to change the brand identity instantly.

    ```css
    :root {
      --first-color: hsl(219, 69%, 56%);
      --first-color-alt: hsl(219, 69%, 52%);
      --title-color: hsl(219, 8%, 95%);
      --text-color: hsl(219, 8%, 75%);
      --body-color: hsl(219, 4%, 4%);
    }
    ```

  * **Adding New Cars:** Copy the article structure within the `.popular__container` div in `index.html`.

    ```html
    <article class="popular__card swiper-slide">
       <div class="shape shape__smaller"></div>
       <h1 class="popular__title">New Model</h1>
       <h3 class="popular__subtitle">Lamborghini</h3>
       <img src="assets/img/new-car.png" alt="" class="popular__img">
       </article>
    ```

  * **Adjusting Animation Speed:** Change the `duration` and `delay` properties in the `ScrollReveal` configuration in `main.js`.

## 🎨 UI/UX Features

  * **Visual Hierarchy:** Uses font weights and color opacity to guide the eye from headers to call-to-action buttons.
  * **Micro-interactions:** Buttons scale slightly on hover; navigation links display a glowing dot indicator.
  * **Neumorphism/Glassmorphism:** The "Features" section uses background blur and semi-transparent borders to create depth.
  * **Consistent Iconography:** Remix Icons provide a cohesive look for battery levels, speedometers, and navigation elements.
  * **Performance:** Images are lazy-loaded (native or via Swiper) to ensure fast First Contentful Paint (FCP).

## ⚡ Key Functions

| Function | Purpose |
| :--- | :--- |
| `scrollHeader()` | Adds a background blur/shadow to the navbar when the user scrolls down \>50px. |
| `scrollActive()` | Detects current viewport section and highlights the corresponding nav link. |
| `mixitup()` | *(Optional)* Can be integrated for filtering car models by category. |
| `Swiper()` | Initializes the touch-slider logic for the "Popular" section. |
| `ScrollReveal()` | Initializes the library that handles entrance animations on scroll. |

## 📱 Responsive Design

The layout utilizes a mobile-first approach with breakpoints for larger screens:

**Mobile (\<767px):**

  * Navigation becomes a bottom-bar or hamburger menu.
  * Grid layouts stack vertically (1 column).
  * Font sizes adjust for readability.

**Tablet (767px - 1023px):**

  * Home image widens.
  * Popular cars display 2 slides per view.
  * Navigation moves to the top right.

**Desktop (\>1024px):**

  * Container width locked for readability.
  * Popular cars display 3 slides per view.
  * Large geometric shapes appear in the background for visual interest.

## 🚀 Future Enhancements

Potential features to add:

  * **3D Viewer:** Integrate Three.js to allow users to rotate the car 360 degrees.
  * **Dark/Light Mode:** A toggle to switch between "Night Drive" and "Day Drive" themes.
  * **Configurator:** A JS-based color picker that changes the car image overlay.
  * **Backend API:** Connect to a CMS to fetch car prices and availability dynamically.
  * **Test Drive Booking:** A modal form with date-picker integration.

-----

*Designed for luxury, built for performance.*