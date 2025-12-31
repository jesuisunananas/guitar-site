
<script lang="ts">
  const links = [
    { href: '#about', label: 'About' },
    { href: '#work',  label: 'Work'  },
    { href: '#contact', label: 'Contact' },
  ];
</script>

<nav class="nav">
  <a class="brand" href="#">Arjun Rewari</a>
  <div class="spacer" />
  {#each links as l}
    <a class="link" href={l.href}>{l.label}</a>
  {/each}
</nav>

<section id="hero" class="hero">
  <h1>Hi, I’m Arjun.</h1>
  <p>I build things for the web.</p>
</section>

<section id="about" class="section">
  <h2>About</h2>
  <p>Short intro about you, skills, and interests.</p>
</section>

<section id="work" class="section">
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
</section>

<section id="contact" class="section">
  <h2>Contact</h2>
  <p>Say hi at <a href="mailto:you@example.com">you@example.com</a>.</p>
</section>

<footer class="footer">
  © {new Date().getFullYear()} Arjun Rewari
</footer>

<style>
  :global(html) { scroll-behavior: smooth; }
  .nav {
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
  .footer { padding: 2rem 1rem; text-align: center; color: #777; }
</style>
