<script>
  let data = [
    {
      title: "Lorem Ipsum 1",
      fill: "Lorem, ipsum dolor sit amet consectetur adipisicing elit. Reprehenderit dolore eveniet quis dolorum, delectus doloremque, nesciunt harum obcaecati velit quidem sunt dignissimos, autem eius iure commodi at sed. Blanditiis, magni.",
    },
    {
      title: "Lorem Ipsum 2",
      fill: "Lorem, ipsum dolor sit amet consectetur adipisicing elit. Reprehenderit dolore eveniet quis dolorum, delectus doloremque, nesciunt harum obcaecati velit quidem sunt dignissimos, autem eius iure commodi at sed. Blanditiis, magni.",
    },
    {
      title: "Lorem Ipsum 3",
      fill: "Lorem, ipsum dolor sit amet consectetur adipisicing elit. Reprehenderit dolore eveniet quis dolorum, delectus doloremque, nesciunt harum obcaecati velit quidem sunt dignissimos, autem eius iure commodi at sed. Blanditiis, magni.",
    },
  ];
</script>

<main class="px-6 py-4">
  <h1 class="font-black text-2xl">Projects</h1>
  <p>
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Officiis, natus sed
    optio reprehenderit voluptatum, asperiores quis eveniet alias voluptatem
    cupiditate inventore aut voluptatibus veniam rerum a provident nisi
    assumenda minus. Veniam porro, perspiciatis aspernatur quod quis similique
    eos illum beatae corporis eveniet quae in pariatur obcaecati sapiente. Vero
    perspiciatis tenetur asperiores nulla amet voluptatum, ipsam voluptate quod
    tempore dicta quibusdam!
  </p>

  <div class="flex flex-row gap-4 mt-4">
    {#each data as item}
      <div class="border rounded w-2xs p-4">
        <h4 class="text-xl">{item.title}</h4>
        <p class="text-sm">
          {item.fill}
        </p>
      </div>
    {/each}
  </div>
</main>
