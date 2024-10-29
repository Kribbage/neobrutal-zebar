<script lang="ts">
  import type { DateOutput, GlazeWmOutput, NetworkOutput } from "zebar";
  import NowPlaying from "./NowPlaying.svelte";

  type RightGroupProps = {
    date: DateOutput;
    glazewm: GlazeWmOutput;
    network: NetworkOutput;
  };

  let { date, glazewm, network }: RightGroupProps = $props();
</script>

<div class="flex flex-row gap-3 items-center">
  <NowPlaying {glazewm} />
  <div class="flex flex-row items-center gap-1">
    {#if network?.defaultInterface?.type === "ethernet"}
      <i class="ti ti-network"></i>
    {:else if network?.defaultInterface!.type === "wifi"}
      {#if network.defaultGateway!.signalStrength! >= 75}
        <i class="ti ti-wifi"></i>
      {:else if network.defaultGateway!.signalStrength! >= 50}
        <i class="ti ti-wifi-2"></i>
      {:else if network.defaultGateway!.signalStrength! >= 25}
        <i class="ti ti-wifi-1"></i>
      {:else}
        <i class="ti ti-wifi-off"></i>
      {/if}
      {network.defaultGateway?.ssid}
    {:else}
      <i class="ti ti-wifi-off"></i>
    {/if}
  </div>
  <i class="ti ti-point-filled"></i>
  {date?.new.toString()}
</div>
