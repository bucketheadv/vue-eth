<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <button @click="open">Connect Wallet</button>
  <vd-board :connectors="connectors" />
  <router-view/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>

<script>
import { CoinbaseWalletConnector, MetaMaskConnector, useBoard, WalletConnectConnector } from 'vue-dapp';
export default {
  name: 'App',
  setup() {
    const { open } = useBoard();
    const infuraId = "";
    const connectors = [
      new MetaMaskConnector({
        appUrl: "http://localhost:3000",
      }),
      new WalletConnectConnector({
        qrcode: true,
        rpc: {
          1: `https://mainnet.infura.io/v3/${infuraId}`,
          4: `https://rinkeby.infura.io/v3/${infuraId}`,
        },
      }),
      new CoinbaseWalletConnector({
        appName: "Vue Dapp",
        jsonRpcUrl: `https://mainnet.infura.io/v3/${infuraId}`,
      }),
    ];
    return {
      connectors,
      open,
    };
  }
}
</script>