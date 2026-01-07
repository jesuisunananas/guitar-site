
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

  const lessons = [
    {
      title: '1-on-1 Private Lessons',
      description: '30 or 60 minute sessions tailored to your pace and goals'
    },
    {
      title: 'In-Person or Online',
      description: 'Studio sessions or convenient Zoom lessons from anywhere'
    },
    {
      title: 'Customized Learning',
      description: 'Practice plans and song-based learning designed for you'
    },
    {
      title: 'Comprehensive Curriculum',
      description: 'Technique, ear training, music theory, and improvisation'
    }
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

  let currentLesson = 0;
  let lessonAutoPlayInterval: number;

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

  function setLesson(index: number) {
    currentLesson = index;
    resetLessonAutoPlay();
  }

  function nextLesson() {
    currentLesson = (currentLesson + 1) % lessons.length;
  }

  function prevLesson() {
    currentLesson = (currentLesson - 1 + lessons.length) % lessons.length;
  }

  function startLessonAutoPlay() {
    lessonAutoPlayInterval = setInterval(nextLesson, 4000);
  }

  function resetLessonAutoPlay() {
    clearInterval(lessonAutoPlayInterval);
    startLessonAutoPlay();
  }

  onMount(() => {
    startAutoPlay();
    startLessonAutoPlay();
  });

  onDestroy(() => {
    clearInterval(autoPlayInterval);
    clearInterval(lessonAutoPlayInterval);
  });

</script>

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

<section id="about" class="section">
  <h2>About</h2>
  <p>
    Riley has been teaching guitar for over 10 years, specializing in rock, blues, and folk.
    Lessons are tailored to each student’s goals, whether that’s learning your first chords
    or improvising over your favorite songs.
  </p>
</section>

<!-- <section id="lessons" class="section">
  <h2>Lessons</h2>
  <ul>
    <li>1-on-1 private lessons (30 or 60 minutes)</li>
    <li>In-person studio sessions or Zoom lessons</li>
    <li>Customized practice plans & song-based learning</li>
    <li>Technique, ear training, music theory, improvisation</li>
  </ul>
</section> -->

<section id="lessons" class="section">
  <h2>Lessons</h2>
  <div class="lessons-carousel">
    <button class="carousel-btn prev" on:click={prevLesson} aria-label="Previous lesson">
      <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
        <path d="M15 18l-6-6 6-6"/>
      </svg>
    </button>
    
    <div class="carousel-content">
      {#key currentLesson}
        <div class="lesson-card" in:fade={{ duration: 300 }}>
          <h3>{lessons[currentLesson].title}</h3>
          <p>{lessons[currentLesson].description}</p>
        </div>
      {/key}
    </div>
    
    <button class="carousel-btn next" on:click={nextLesson} aria-label="Next lesson">
      <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
        <path d="M9 18l6-6-6-6"/>
      </svg>
    </button>
  </div>
  
  <div class="lesson-indicators">
    {#each lessons as _, index}
      <button
        class="indicator-dot"
        class:active={index === currentLesson}
        on:click={() => setLesson(index)}
        aria-label="View lesson {index + 1}"
      ></button>
    {/each}
  </div>
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
  
  /* Hide the outline on a mouse click */
  *:focus:not(:focus-visible) {
    outline: none;
  }
  /* Provide clear focus styles for keyboard users */
  *:focus-visible {
    outline: 2px solid #2563eb;
    outline-offset: 2px;
  }
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
    padding: 1rem 1rem;
  }

  .hero p {
    font-size: 1.3rem;
    line-height: 1.4;
    margin: 0.5rem 0;
  }

  .section {
    padding: 2rem 1rem;
    max-width: 900px;
    margin: 0 auto;
  }

  .section h2 {
    text-align: center;
    font-size: 2rem;
    margin-bottom: 2rem;
    color: #1a1a1a;
  }

  /* About Section Specific Styles */
  #about {
    padding-bottom: 2rem;
  }

  #about p {
    font-size: 1.2rem;
    line-height: 1.8;
  }

  /* Lessons Section Specific Styles */
  #lessons {
    padding-top: 2rem;
    padding-bottom: 3rem;
  }

  /* Lessons Carousel */
  .lessons-carousel {
    display: flex;
    align-items: center;
    gap: 1rem;
    margin: 2rem auto;
    max-width: 600px;
  }

  .carousel-btn {
    background-color: #ffffff;
    border: 1px solid #e5e7eb;
    border-radius: 50%;
    width: 56px;
    height: 56px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: all 0.3s ease;
    flex-shrink: 0;
    color: #1a1a1a;
  }

  .carousel-btn:hover {
    background-color: #f9fafb;
    border-color: #2563eb;
    color: #2563eb;
    transform: scale(1.05);
  }

  .carousel-btn:active {
    transform: scale(0.95);
  }

  .carousel-content {
    flex: 1;
    min-height: 200px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .lesson-card {
    background-color: #ffffff;
    padding: 2rem;
    border-radius: 12px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    border: 1px solid #e5e7eb;
    text-align: center;
    width: 100%;
  }

  .lesson-card h3 {
    margin: 0 0 0.75rem 0;
    color: #1a1a1a;
    font-size: 1.5rem;
    font-weight: 600;
  }

  .lesson-card p {
    margin: 0;
    color: #6b7280;
    line-height: 1.6;
    font-size: 1.1rem;
  }

  .lesson-indicators {
    display: flex;
    gap: 0.5rem;
    justify-content: center;
    align-items: center;
    margin-top: 1.5rem;
  }

  .indicator-dot {
    width: 10px;
    height: 10px;
    background-color: #cbd5e0;
    border: none;
    border-radius: 50%;
    cursor: pointer;
    transition: all 0.3s ease;
    padding: 0;
  }

  .indicator-dot:hover {
    background-color: #a0aec0;
    transform: scale(1.2);
  }

  .indicator-dot.active {
    background-color: #2563eb;
    transform: scale(1.3);
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
    color: #1a1a1a;
    font-size: 2rem;
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
    }
    to {
      opacity: 1;
    }
  }

  .author {
    margin-top: 1.3rem;
    font-size: 1rem;
    line-height: 1.25rem;
    color: rgba(107, 114, 128, 1);
    font-style: italic;
  }

  /* Responsive adjustments */
  @media (max-width: 640px) {
    .lessons-carousel {
      gap: 0.5rem;
    }

    .carousel-btn {
      width: 40px;
      height: 40px;
    }

    .lesson-card {
      padding: 1.5rem;
    }

    .lesson-card h3 {
      font-size: 1.25rem;
    }

    .lesson-card p {
      font-size: 1rem;
    }
  }

</style>