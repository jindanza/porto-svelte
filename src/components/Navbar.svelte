<script>
  import Button from "./ui/Button.svelte";
</script>

<nav
  class="flex justify-between px-6 py-4 bg-[#0E1116] text-white fixed top-0 left-0 w-full"
>
  <h1 class="font-black text-2xl">MJDN</h1>
  <ul class="flex gap-4 items-center">
    <li>About</li>
    <li>Profile</li>
    <li>Projects</li>
    <li>Experiences</li>
    <li><Button>Contact</Button></li>
  </ul>
</nav>
