<script lang="ts">
  import { onMount } from 'svelte';

  let peer:any;
  let peerId = '';
  let connection;

  onMount(() => {
    import('peerjs').then(({ Peer }) => {
      peer = new Peer();
      peer.on('open', (id:string) => {
        console.log('My peer ID is: ' + id);
      });
    });
  });

  function connectToPeer(peerId: string) {
    console.log('connectToPeer', peerId, peer);
    if (peer) {
      connection = peer.connect(peerId);
    }
  }
</script>

<input type="text" placeholder="Enter a peer ID" bind:value="{peerId}" />
<button on:click="{() => connectToPeer(peerId)}">Connect</button>
