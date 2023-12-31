# horde.js

JS/TS Wrapper for the Stable Horde API. With internal caching and typings. Suitable for Server and Client applications.

## Usage

```ts
  import {HordeClient, samplers, postProcessors, type GenerationInputStable, type PostProcessors} from 'horde.js'
  const hordeClient = new HordeClient(
    PUBLIC_HORDE_CLIENT_NAME,
    PUBLIC_HORDE_CLIENT_VERSION,
    PUBLIC_HORDE_CLIENT_CONTACT
  )
  const token = $page.data.user.hordeKey || "0000000000"
    let genReq: GenerationInputStable = {
    prompt: "",
    models: ["stable_diffusion"],
    nsfw: false,
    trusted_workers: false,
    slow_workers: true,
    censor_nsfw: true,
    workers: [],
    worker_blacklist: false,
    source_image: "",
    source_processing: "img2img",
    source_mask: "",
    r2: true,
    shared: true,
    replacement_filter: false,
    dry_run: false,
    params: {
      sampler_name: "k_euler_a",
      cfg_scale: 7.5,
      denoising_strength: 0.75,
      seed: "",
      height: 512,
      width: 512,
      seed_variation: 1,
      post_processing: ["GFPGAN"],
      karras: false,
      tiling: false,
      hires_fix: false,
      clip_skip: 1,
      // control_type: "normal",
      // image_is_control: false,
      // return_control_map: false,
      facefixer_strength: 0.5,
      loras: [],
      tis: [],
      special: {},
      steps: 30,
      n: 1
    }
  }
  async function submitReq() {
    genReq.prompt = `${prompt} ${negativePrompt !== "" ? ` ### ${negativePrompt}` : ""}`
    if (!genReq.params) {
      genReq.params = {}
    }
    console.log("ran on token", token, genReq)
    const res = await hordeClient.asyncImageGen(token, genReq, (e) => {
      console.log(e)
    },  (e) => {
      console.log(e)
      e.generations.forEach((gen) => {
        // where update images is a function that loads images into the dom
        updateImages([...activeImages, gen.img])
      })
    }, (e) => {
      console.log(e)
    }, (e) => {
      console.log(e)
    })
    console.log(res)
  }
```

## Conception 
This wrapper was made for my diffusion project... available at https://github.com/ghorde/diffusion

Tried to use the wrapper already available, but failed.

## Contribution Guidelines

Please use JSDoc and TypeScript to their maximum, document everything well and keep name schemes consistent.

