<script lang="ts">
  import "twind/shim"
  import { tw } from "twind"
  import logo from "./assets/svelte.png"
  import Head from "./lib/Head.svelte"
  import Kofi from "./lib/Kofi.svelte"
  import Menu from "./lib/Menu.svelte"
  import Social from "./lib/Social.svelte"
  import { fly, fade } from "svelte/transition"
  import { onMount, tick } from "svelte"

  const url = "https://why-i-want-keychron.vercel.app"
  const title = "Why I want Keychron?"

  const menuItems = [{ name: "ทวีต", url: "https://github.com/narze/why-i-want-keychron" }]

  const description = "Why I want Keychron?"
  const imageUrl =
    "https://raw.githubusercontent.com/narze/timelapse/master/projects/why-i-want-keychron_home.png"
  const gtagId = null

  const reasons = [
    "จะเอาให้แฟนใช้",
    "อยากใช้กับหลายๆ Device พร้อมกัน",
    "พกพาสะดวก",
    "วัสดุเกรดอากาศยาน!",
    "ฉันเป็น 9ทุน",
    "แป้นพิมพ์ภาษาไทย ดีไซน์เฉียบ",
    "ต่อ iPad ได้ง่าย",
    "ถ้าได้ฟรีก็จะได้ไม่ต้องซื้อเอง",
  ]

  let loaded = false
  let reason

  onMount(() => {
    randomReason()
  })

  async function randomReason() {
    loaded = false
    reason = reasons[Math.floor(Math.random() * reasons.length)]
    await tick()
    loaded = true
  }

  function splitWord(word: string) {
    const alphas = word.split("")
    const out = []

    alphas.forEach((a) => {
      if (a.match(/[ก-ฮa-zA-Z]/) || a.match(/[ใเแโไาำะๆฯฤา]/)) {
        out.push(a)
      } else {
        out[out.length - 1] += a
      }
    })

    return out
  }
</script>

<!-- <Kofi name="narze" label="Support Me" /> -->
<!-- <Menu items={menuItems} /> -->
<!-- <Social {url} {title} /> -->
<Head {title} {description} {url} {imageUrl} {gtagId} />

<main class="w-full h-screen overflow-hidden flex flex-col justify-center items-center bg-gray-900">
  <h1 class="text-6xl flex flex-col">
    {#if loaded}
      <span in:fly={{ x: 500, y: 100, duration: 1000, delay: 0 }}>อยากได้</span>
      <span in:fly={{ x: 500, y: 100, duration: 1000, delay: 1000 }}><strong>Keychron</strong></span
      >
      <span in:fly={{ x: 500, y: 100, duration: 1000, delay: 2000 }}>เพราะ...</span>
      <span
        class="reason animate-bounce bg-white rounded rounded-lg p-4"
        style={`font-size: ${140 / splitWord(reason).length}vmin;`}
        in:fly={{ x: 500, y: 100, duration: 1000, delay: 3000 }}>{reason}</span
      >
      <button
        class="mt-2 -mb-12 inline-block cursor-pointer rounded-md bg-gray-800 px-4 py-3 text-center text-sm font-semibold uppercase text-white transition duration-200 ease-in-out hover:bg-gray-900"
        in:fade={{ duration: 1000, delay: 4000 }}
        on:click={randomReason}>สุ่มใหม่</button
      >
    {/if}
  </h1>
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell,
      "Open Sans", "Helvetica Neue";
    font-size: 4vmin;
    color: #ff7d00;
  }

  .reason {
    margin-top: 5vmin;
  }
</style>
