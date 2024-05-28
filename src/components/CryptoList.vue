<template>
    <div>
        <h1 class="text-2xl font-bold mb-4">Cryptocurrency Prices</h1>
        <button @click="fetchData" class="mb-4 px-4 py-2 bg-blue-500 text-white rounded">Get Data</button>
        <div v-if="loading" class="text-center">Loading...</div>
        <table v-else class="table-auto w-full border border-collapse border-gray-500">
            <thead>
                <tr>
                    <th class="px-4 py-2 border border-gray-500">Rank</th>
                    <th class="px-4 py-2 border border-gray-500">Name</th>
                    <th class="px-4 py-2 border border-gray-500">Symbol</th>
                    <th class="px-4 py-2 border border-gray-500">Price (USD)</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="crypto in cryptos" :key="crypto.id">
                    <td class="border px-4 py-2 border-gray-500">{{ crypto.rank }}</td>
                    <td class="border px-4 py-2 border-gray-500">{{ crypto.name }}</td>
                    <td class="border px-4 py-2 border-gray-500">{{ crypto.symbol }}</td>
                    <td class="border px-4 py-2 border-gray-500">{{ crypto.price_usd }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            cryptos: [],
            loading: true
        };
    },
    methods: {
        async fetchData() {
            this.loading = true;
            try {
                const response = await fetch('https://api.coinlore.net/api/tickers/');
                const data = await response.json();
                this.cryptos = data.data;
            } catch (error) {
                console.error('Error fetching data:', error);
            } finally {
                this.loading = false;
            }
        }
    },
    mounted() {
        this.fetchData();
    }
};
</script>
  
<style scoped>
table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 1rem;
}

th,
td {
    border: 1px solid #4A5568;
    /* warna gray-600 */
    padding: 0.5rem;
    text-align: left;
}

th {
    background-color: #2D3748;
    /* warna gray-800 */
    color: #F7FAFC;
    /* warna white */
}

button {
    background-color: blue;
    color: white;
    padding: 20px;
}</style>
  