<template>
  <div>
    <svg ref="svg" xmlns="http://www.w3.org/2000/svg" version="1.1" viewBox="0 0 428.55618 58.657055">
      <path style="fill:#fdf7e5"
            d="m0 1.2521 11.599-0.3071 4.7247 1.063 9.2132-0.82682 9.2368 3.9215 8.41-0.21261 13.276-3.9924 23.033-0.0709 11.198 3.1892 42.357-1.252 14.032-2.6458l17.98-0.1182 116.91 4.5357 31.963-1.3465 13.324-1.9371 23.033-0.35435 6.7799 1.8426 21.427-0.0709 5.7169-2.0316 28.915-0.47247 5.4098 2.4096 9.9455-0.4016 0.0472 46.562-6.6855-0.0709-6.9689 1.7954-11.599 0.0236-10.772-1.7009-16.655 3.6144-8.6462-1.2284-37.349 0.73233-11.103-1.7954-12.379 4.0396-12.45-1.9608-18.427 2.2749-46.49 1.3395-11.937-1.7495-20.222-0.25986-11.544 0.96996-68.933-0.8032-9.4967 2.386-8.8824 0.0472-4.5121-1.5355-29.246 1.7245-4.7011 1.7481-37.302-0.89769-3.7798 1.2284-18.261-0.47247z"/>
      <path style="stroke:#7eacf7;stroke-width:.99979;fill:none" d="m0.052917 13.764h428.51"/>
      <path style="stroke:#7eacf7;stroke-width:.99979;fill:none" d="m0.052917 41.545h428.51"/>
      <path style="stroke:#e58483;stroke-width:.99262;fill:none" d="m42.858 4.7176v53.26"/>
      <text y="40.136166" x="52.387501"
            style="font-family: 'LC', serif;font-variant-ligatures:normal;font-size:31.75px;font-variant-numeric:normal;letter-spacing:0px;line-height:1.25;word-spacing:0px;font-variant-caps:normal;font-feature-settings:normal;fill:#000000">
        <tspan x="52.387501"
               style="font-size:31.75px;font-variant-numeric:normal;font-variant-ligatures:normal;font-variant-caps:normal;font-feature-settings:normal;stroke-width:.26458"
               y="40.136166"
               :text-decoration="done ? 'line-through' : ''"
        >
          {{editableContent}}
        </tspan>
      </text>
    </svg>
    <div class="input">
      <input type="checkbox" v-model="done"/>
      <input type="text" ref="input" v-model="editableContent"/>
      <button @click="savePng">Download as PNG</button>
      <button @click="viewPng">View as PNG</button>
    </div>
    <img ref="view"/>
  </div>
</template>

<script>
  import svg from 'save-svg-as-png'
  import fromHtml from 'html-to-image'

  const insertAt = (str, sub, pos) => `${str.slice(0, pos)}${sub}${str.slice(pos)}`;

  export default {
    name: "Item",
    props: {
      content: {type: String, default: 'lock the groundskeeper out of the garden'},
    },
    data () {
      return {
        editableContent: this.content,
        done: false,
      }
    },
    methods: {
      savePng () {
        svg.saveSvgAsPng(this.$refs.svg, 'todo.png', {scale: 2.3})
      },
      async viewPng () {
        this.$refs.view.src = await svg.svgAsPngUri(this.$refs.svg, {scale: 2.3})
      }
    },
    computed: {},
  }
</script>

<style lang="scss">
  img {
    max-width: 100%;
  }
  .input {
    display: flex;
    width: 100%;
    max-width: 60em;
    align-items: center;
    justify-content: center;
    margin: auto;

    input[type="text"] {
      flex-grow: 1;
    }
  }
</style>
