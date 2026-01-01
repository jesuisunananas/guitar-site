
<script lang="ts">
  import { onMount, onDestroy } from 'svelte';
  import { fade } from 'svelte/transition';
  import guyPlaying from './assets/guy_playing.jpg';
  import img1 from './assets/img1.png';

  const links = [
    { href: '#about', label: 'About' },
    { href: '#gallery',  label: 'Gallery'  },
    { href: '#contact', label: 'Contact' },
  ];

  const videos = [
  {
    title: 'Beginner Fingerstyle Lesson',
    url: 'https://www.youtube.com/embed/dQw4w9WgXcQ'
  },
  {
    title: 'Blues Improvisation Demo',
    url: 'https://www.youtube.com/embed/dQw4w9WgXcQ'
  },
  {
    title: 'Blues Improvisation Demo',
    url: 'https://www.youtube.com/embed/dQw4w9WgXcQ'
  },
  {
    title: 'Blues Improvisation Demo',
    url: 'https://www.youtube.com/embed/dQw4w9WgXcQ'
  }
  ];

  const profile_photo = [
    { alt: 'Guitar Teacher Profile Shot', src: guyPlaying}
  ]

  const photos = [
    { alt: 'Teaching a student', src: img1}
  ];

  const testimonials = [
    {
      text: "Riley is an excellent guitar teacher. He is very patient and works with whatever level you are at. I have been learning guitar from for over a year. I started as a complete novice and have learnt to read music and play several tunes on the acoustic guitar.",
      author: "Rohini R"
    },
    {
      text: "Best guitar teacher I've ever had! Riley's passion for music is contagious, and he really knows how to adapt lessons to your skill level and musical interests.",
      author: "Michael Chen"
    },
    {
      text: "I went from struggling with basic chords to playing my favorite songs confidently. Riley's structured approach and encouragement kept me motivated throughout my learning journey.",
      author: "Emma Rodriguez"
    }
  ];
  
  let currentTestimonial = 0;
  let autoPlayInterval: number;

  function setTestimonial(index: number) {
    currentTestimonial = index;
    resetAutoPlay();
  }

  function nextTestimonial() {
    currentTestimonial = (currentTestimonial + 1) % testimonials.length;
  }

  function startAutoPlay() {
    autoPlayInterval = setInterval(nextTestimonial, 5000);
  }

  function resetAutoPlay() {
    clearInterval(autoPlayInterval);
    startAutoPlay();
  }

  onMount(() => {
    startAutoPlay();
  });

  onDestroy(() => {
    clearInterval(autoPlayInterval);
  });

</script>

<!-- <nav class="nav">
  <a class="brand" href="#">Arjun Rewari</a>
  <div class="spacer" />
  {#each links as l}
    <a class="link" href={l.href}>{l.label}</a>
  {/each}
</nav> -->

<section id="title-header" class="title-header">
  <h1>Riley Merlino</h1>
</section>

<section id="profile-photo" class="profile-photo">
  {#each profile_photo as p}
    <img src={p.src} alt={p.alt} />
  {/each}
</section>

<section id="hero" class="hero">
  <p>Private guitar lessons for beginners & intermediate players.</p>
  <p>In-person and online • Acoustic & electric • All ages welcome.</p>
</section>

<!-- <section id="hero" class="hero">
  <h1>Hi, I’m Arjun.</h1>
  <p>I build things for the web.</p>
</section> -->

<section id="about" class="section">
  <h2>About</h2>
  <p>
    Riley has been teaching guitar for over 10 years, specializing in rock, blues, and folk.
    Lessons are tailored to each student’s goals, whether that’s learning your first chords
    or improvising over your favorite songs.
  </p>
</section>

<section id="lessons" class="section">
  <h2>Lessons</h2>
  <ul>
    <li>1-on-1 private lessons (30 or 60 minutes)</li>
    <li>In-person studio sessions or Zoom lessons</li>
    <li>Customized practice plans & song-based learning</li>
    <li>Technique, ear training, music theory, improvisation</li>
  </ul>
</section>

<section id="videos" class="section">
  <h2>Videos</h2>
  <div class="video-grid">
    {#each videos as v}
      <div class="video-card">
        <div class="video-wrapper">
          <iframe
            src={v.url}
            title={v.title}
            frameborder="0"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen
          ></iframe>
        </div>
        <p class="video-title">{v.title}</p>
      </div>
    {/each}
  </div>
</section>

<section id="testimonials" class="testimonials-section">
  <h2>Testimonials</h2>
  <div class="testimonial-container">
    {#key currentTestimonial}
      <div class="card" in:fade>
        <!-- <div class="stars">
          {#each Array(testimonials[currentTestimonial].rating) as _}
            <svg class="star" viewBox="0 0 20 20" fill="currentColor">
              <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
            </svg>
          {/each}
        </div> -->
        <div class="infos">
          <!-- <p class="date-time">{testimonials[currentTestimonial].date}</p> -->
          <p class="description">{testimonials[currentTestimonial].text}</p>
          <p class="author">— {testimonials[currentTestimonial].author}</p>
        </div>
      </div>
    {/key}
    
    <div class="testimonial-indicators">
      {#each testimonials as _, index}
        <button
          class="indicator-line"
          class:active={index === currentTestimonial}
          on:click={() => setTestimonial(index)}
          aria-label="View testimonial {index + 1}"
        ></button>
      {/each}
    </div>
  </div>
</section>

<!-- <section id="work" class="section">
  <h2>Selected Work</h2>
  <ul class="cards">
    <li class="card">
      <h3>Project One</h3>
      <p>One-liner about what it is and your role.</p>
      <a href="#" target="_blank" rel="noreferrer">View</a>
    </li>
    <li class="card">
      <h3>Project Two</h3>
      <p>Another short description.</p>
      <a href="#" target="_blank" rel="noreferrer">View</a>
    </li>
  </ul>
</section> -->


<section id="booking" class="section">
  <h2>Book a Lesson</h2>
  <p>
    Choose a time that works for you using the calendar below.
  </p>
  <a
    class="booking-button"
    href="https://calendar.google.com/calendar/appointments/s/EXAMPLE_BOOKING_LINK"
    target="_blank"
    rel="noreferrer"
  >
    Open Booking Calendar
  </a>
</section>

<section id="contact" class="section">
  <h2>Contact</h2>
  <p>Email: <a href="mailto:rileymerlino@gmail.com">rileymerlino@gmail.com</a></p>
  <p>Phone: XXX-XXX-XXX </p>
  <p>Instagram: <a href="https://instagram.com/username" target="_blank" rel="noreferrer">@username</a></p>
</section>

<style>
  :global(html) { scroll-behavior: smooth; }
  :global(body) { margin: 0; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif; }
  
  .title-header {
    text-align: center;
    padding: 2rem 1rem;
  }

  .profile-photo {
    text-align: center;
    padding: 1rem;
  }

  .hero {
    text-align: center;
    padding: 2rem 1rem;
  }

  .section {
    padding: 4rem 1rem;
    max-width: 900px;
    margin: 0 auto;
  }

  .video-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
    margin-top: 2rem;
  }

  .video-wrapper {
    position: relative;
    padding-bottom: 56.25%;
    height: 0;
    overflow: hidden;
  }

  .video-wrapper iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }

  .video-title {
    margin-top: 0.5rem;
    font-weight: 500;
  }

  .booking-button {
    display: inline-block;
    margin-top: 1rem;
    padding: 0.75rem 1.5rem;
    background-color: #2563eb;
    color: white;
    text-decoration: none;
    border-radius: 8px;
    font-weight: 500;
    transition: background-color 0.3s;
  }

  .booking-button:hover {
    background-color: #1d4ed8;
  }

  /* Testimonials Section */
  .testimonials-section {
    padding: 4rem 1rem;
    max-width: 1000px;
    margin: 0 auto;
  }

  .testimonials-section h2 {
    text-align: center;
    margin-bottom: 3rem;
    font-size: 2rem;
    color: #1a1a1a;
  }

  .testimonial-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2rem;
  }

  .card {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    background-color: rgba(255, 255, 255, 1);
    padding: 30px;
    max-width: 400px;
    width: 100%;
    border-radius: 12px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    min-height: 280px;
  }

  .infos {
    margin-top: 1rem;
  }

  .description {
    margin-top: 0.4rem;
    line-height: 1.625;
    font-size: 1.1rem;
    color: rgba(107, 114, 128, 1);
  }

  .author {
    margin-top: 1.3rem;
    font-size: 1rem;
    line-height: 1.25rem;
    color: rgba(107, 114, 128, 1);
  }

  .testimonial-indicators {
    display: flex;
    gap: 0.5rem;
    justify-content: center;
    align-items: center;
  }

  .indicator-line {
    width: 24px;
    height: 3px;
    background-color: #cbd5e0;
    border: none;
    border-radius: 2px;
    cursor: pointer;
    transition: all 0.3s ease;
    padding: 0;
  }

  .indicator-line:hover {
    background-color: #a0aec0;
  }

  .indicator-line.active {
    width: 40px;
    background-color: rgba(7, 63, 216, 1);
  }

  @keyframes fade {
    from {
      opacity: 0;
      transform: translateY(10px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  .card {
    animation: fade 0.5s ease-in-out;
  }
</style>