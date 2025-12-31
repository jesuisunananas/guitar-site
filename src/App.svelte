
<script lang="ts">
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
  }
  ];

  const profile_photo = [
    { alt: 'Guitar Teacher Profile Shot', src: guyPlaying}
  ]

  const photos = [
    { alt: 'Teaching a student', src: img1}
  ];
</script>

<nav class="nav">
  <a class="brand" href="#">Arjun Rewari</a>
  <div class="spacer" />
  {#each links as l}
    <a class="link" href={l.href}>{l.label}</a>
  {/each}
</nav>

<section id="title-header" class="title-header">
  <h1>John Doe – Guitar Teacher</h1>
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
    John has been teaching guitar for over 10 years, specializing in rock, blues, and folk.
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
  <p>Email: <a href="mailto:guitar.teacher@example.com">guitar.teacher@example.com</a></p>
  <p>Instagram: <a href="https://instagram.com/username" target="_blank" rel="noreferrer">@username</a></p>
</section>

<style>
  :global(html) { scroll-behavior: smooth; }
  /* .nav {
    position: sticky; top: 0; backdrop-filter: blur(6px);
    display: flex; align-items: center; gap: 1rem;
    padding: 0.75rem 1rem; border-bottom: 1px solid #161616;
  }
  .brand { font-weight: 700; text-decoration: none; color: inherit; }
  .spacer { flex: 1; }
  .link { text-decoration: none; color: #121111; margin-left: 1rem; }
  .hero {
    min-height: 65vh; display: grid; place-content: center;
    text-align: center; padding: 4rem 1rem;
  }
  .section { padding: 4rem 1rem; max-width: 900px; margin: 0 auto; }
  .cards { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 1rem; padding: 0; list-style: none; }
  .card { border: 1px solid #eee; padding: 1rem; border-radius: 12px; }
  .footer { padding: 2rem 1rem; text-align: center; color: #777; }*/
</style>