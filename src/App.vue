<template>
  <div id="app">
    <div class="container">
      <h1>Asset List</h1>
      <main>
        <table>
          <thead>
            <tr>
              <th>Asset Name</th>
              <th>Department</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(department, assetName) in assets" :key="assetName">
              <td>{{ assetName }}</td>
              <td>{{ department }}</td>
            </tr>
          </tbody>
        </table>
        <button @click="downloadCSV">Download CSV</button>
      </main>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      assets: {
        "Printer": "HR",
        "Monitor": "IT",
        "Barcode Scanner": "ACCOUNT"
      }
    };
  },
  methods: {
    downloadCSV() {
      let csvContent = "Asset Name,Department\n";
      for (const [assetName, department] of Object.entries(this.assets)) {
        csvContent += `${assetName},${department}\n`;
      }

      const blob = new Blob([csvContent], { type: "text/csv;charset=utf-8;" });
      const link = document.createElement("a");
      link.href = URL.createObjectURL(blob);
      link.setAttribute("download", "assets.csv");
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    }
  }
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html, body {
  height: 100%;
  margin: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  background: linear-gradient(135deg, #f0f4f8, #e8eff4);
  font-family: 'Arial', sans-serif;
  color: #333;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
}

.container {
  width: 100%;
  max-width: 1200px;
  padding: 20px;
  border-radius: 12px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background: transparent;
}

h1 {
  font-size: 2.5rem;
  font-weight: bold;
  color: #4CAF50;
  margin-bottom: 20px;
  text-transform: uppercase;
  letter-spacing: 2px;
  text-shadow: 2px 2px 8px rgba(0, 0, 0, 0.1);
  text-align: center;
}

main {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

table {
  margin-top: 20px;
  width: 100%;
  border-collapse: collapse;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  background: transparent;
}

th, td {
  border: 1px solid #ddd;
  padding: 12px;
  text-align: left;
  font-size: 1.1rem;
}

th {
  background-color: #4CAF50;
  color: white;
  font-weight: bold;
}

td {
  background-color: #f9f9f9;
  color: black;
  font-weight: bold;
}

tr:nth-child(even) td {
  background-color: #f1f1f1;
}

tr:hover td {
  background-color:rgb(0, 105, 56);
}

button {
  margin-top: 20px;
  padding: 12px 24px;
  cursor: pointer;
  font-size: 16px;
  border: none;
  border-radius: 6px;
  background-color: #4CAF50;
  color: white;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #45a049;
}

@media (min-width: 1920px) {
  h1 {
    font-size: 3rem;
  }

  table {
    font-size: 1.3rem;
  }

  button {
    font-size: 18px;
  }
}
</style>
