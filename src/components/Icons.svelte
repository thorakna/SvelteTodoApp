<script lang="ts">
    export let name: string;
    export let width = "1.5rem";
    export let height = "1.5rem";
    let icons = [
      {
        box: 24,
        name: "check-mark",
        svg: `<svg focusable="false" viewBox="0 0 24 24" aria-hidden="true"><path d="M19.77 4.93l1.4 1.4L8.43 19.07l-5.6-5.6 1.4-1.4 4.2 4.2L19.77 4.93m0-2.83L8.43 13.44l-4.2-4.2L0 13.47l8.43 8.43L24 6.33 19.77 2.1z"></path></svg>`,
      },
      {
        box: 24,
        name: "check-mark-fill",
        svg: `<svg focusable="false" viewBox="0 0 24 24" aria-hidden="true"><path d="M 20.084 3.399 L 21.484 4.799 C 18.328 -2.633 7.166 18.591 8.744 17.539 C 17.551 10.689 8.342 14.649 7.485 12.926 L 3.163 12.906 C 2.9 13.958 10.257 14.41 10.52 13.358 L 20.084 3.399 M 20.084 0.569 L 8.744 11.909 L 4.544 7.709 L 0.314 11.939 L 8.744 20.369 L 24.314 4.799 L 20.084 0.569 Z"></path></svg>`,
      },
      {
        box: 32,
        name: "delete",
        svg: `<svg focusable="false" viewBox="0 0 24 24" aria-hidden="true"><path d="M6 19c0 1.1.9 2 2 2h8c1.1 0 2-.9 2-2V7H6v12zM8 9h8v10H8V9zm7.5-5l-1-1h-5l-1 1H5v2h14V4h-3.5z"></path></svg>`,
      },
    ];
    let displayIcon: any;
    $: displayIcon = icons.find((e) => e.name === name);
  </script>
  
  <svg
    class={$$props.class}
    {width}
    {height}
    viewBox="0 0 {displayIcon.box} {displayIcon.box}">{@html displayIcon.svg}</svg
  >  