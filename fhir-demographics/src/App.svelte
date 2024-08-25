<script lang="ts">
  import svelteLogo from './assets/svelte.svg'
  import viteLogo from '/vite.svg'
  import Counter from './lib/Counter.svelte'
  import 'medblocks-ui'
  import '@shoelace-style/shoelace/dist/themes/light.css'
  import axios from "axios";
  import './tailwind.css'


  let loading:boolean = false;

  async function handleSubmit(e: any) {
    console.log('Submit event triggered');
    console.log('Form data:', e.detail);
    const r= await axios.post("http://localhost:8090/fhir/Patient", e.detail)
    console.log(r.data);
  }

</script>
<div class="container mx-auto p-4 sm:px-8 max-w-7xl py-10">
  <h1 class="text-2xl font-semibold font-sans">Patient Registration</h1>
  <mb-fhir-form class="flex flex-col gap-3" on:mb-submit={handleSubmit}>
  <mb-context>path="resourceType" data="Patient"</mb-context>
  <mb-input path="name[0].given" label="Name"></mb-input>
  <mb-date label="Date of birth" path="birthDate"></mb-date>
  <mb-buttons type="code" label="Gender" path="gender">
    <mb-option value="male" label="Male"></mb-option>
    <mb-option value="female" label="Female"></mb-option>
    <mb-option value="other" label="Other"></mb-option>
  </mb-buttons>
  <mb-submit>
    <sl-button type="info">Submit</sl-button>
  </mb-submit>
  </mb-fhir-form>
</div>

