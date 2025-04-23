<script>
  import Button from "./ui/Button.svelte";
  import { onMount, onDestroy } from "svelte";

  let modelViewer;
  let animationFrame;

  const sensitivity = -3;

  let currentRotation = 0;
  let targetRotation = 0;
  let scrollRotationActive = false;

  // Easing: easeInOutQuad
  function easeInOutQuad(t) {
    return t < 0.5 ? 2 * t * t : -1 + (4 - 2 * t) * t;
  }

  // Intro animation
  const duration = 2000;
  let startTime = null;

  function animateIntro(timestamp) {
    if (!startTime) startTime = timestamp;

    const elapsed = timestamp - startTime;
    const progress = Math.min(elapsed / duration, 1);
    const easedProgress = easeInOutQuad(progress);

    const rotation = easedProgress * 360;

    if (modelViewer) {
      modelViewer.style.opacity = easedProgress;
      modelViewer.setAttribute(
        "camera-orbit",
        `${rotation.toFixed(2)}deg 100deg 0m`
      );
    }

    if (progress < 1) {
      animationFrame = requestAnimationFrame(animateIntro);
    } else {
      // setelah animasi awal selesai, aktifkan scroll rotasi
      scrollRotationActive = true;
      animationFrame = requestAnimationFrame(animateScrollRotation);
    }
  }

  // Smooth scroll-based rotation
  function animateScrollRotation() {
    currentRotation = lerp(currentRotation, targetRotation, 0.05);
    if (modelViewer) {
      modelViewer.setAttribute(
        "camera-orbit",
        `${currentRotation.toFixed(2)}deg 100deg 0m`
      );
    }
    animationFrame = requestAnimationFrame(animateScrollRotation);
  }

  const lerp = (a, b, t) => a + (b - a) * t;

  function handleScroll() {
    if (scrollRotationActive) {
      const scrollY = window.scrollY;
      targetRotation = (scrollY / sensitivity) % 360;
    }
  }

  onMount(() => {
    if (!customElements.get("model-viewer")) {
      const script = document.createElement("script");
      script.src =
        "https://unpkg.com/@google/model-viewer@latest/dist/model-viewer.min.js";
      script.type = "module";
      document.head.appendChild(script);
    }

    window.addEventListener("scroll", handleScroll);

    // mulai dengan animasi intro
    animationFrame = requestAnimationFrame(animateIntro);

    onDestroy(() => {
      window.removeEventListener("scroll", handleScroll);
      cancelAnimationFrame(animationFrame);
    });
  });
</script>

<main class="flex h-screen items-center bg-[#0E1116]">
  <div>
    <div class="px-6 py-4 text-white">
      <div>
        <model-viewer
          bind:this={modelViewer}
          src="/src/assets/old_computers.glb"
          alt="TVs"
          disable-pan
          disable-zoom
          interaction-prompt="none"
          camera-orbit="0deg 100deg 0m"
          camera-target="0m 10m 0m"
          field-of-view="20deg"
          style="width: 100%; height: 100%; position: absolute; z-index:1; top: 0; right:0; opacity: 0; transition: opacity 0.5s ease-in-out;"
        >
        </model-viewer>
        <div style="position: absolute; z-index: 10; top:200px; right: 0;">
          <h1 class="font-black text-6xl">Muhammad Jindan</h1>
          <p class="text-2xl mb-4 mt-2">Software Engineer</p>
          <p class="mb-4">
            A passionate and problem-solving-oriented Software Engineer who is
            committed to continuously developing knowledge and skills,
            delivering clean code, and learning new technologies.
          </p>
          <Button>Review CV</Button>
        </div>
      </div>
    </div>
  </div>
</main>
