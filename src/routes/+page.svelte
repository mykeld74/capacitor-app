<script lang="ts">
  import { Geolocation } from "@capacitor/geolocation";
  import { onMount } from "svelte";

  interface Location {
    coords: {
      latitude: number | null | undefined;
      longitude: number | null | undefined;
      accuracy: number | null | undefined;
      altitude: number | null | undefined;
      altitudeAccuracy: number | null | undefined;
      speed: number | null | undefined;
    };
    timestamp: number;
  }
  let loc: Location | null = null;
  async function getCurrentLocation() {
    const res = await Geolocation.getCurrentPosition();
    loc = res;
  }

  onMount(() => {
    getCurrentLocation();
  });
</script>

<div>
  <h1>Geolocation</h1>
  <p>Your location is:</p>
  <p>Latitude: {loc?.coords.latitude}</p>
  <p>Longitude: {loc?.coords.longitude}</p>

  <button on:click={getCurrentLocation}>Get Location</button>
</div>
