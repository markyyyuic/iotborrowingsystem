<template>

  <!-- SIDE BAR SECTION -->
  <div class="side-bar">

    <div class="logo-container">
      <img src="../assets/loginlogo.png" alt="">
    </div>

    <div class="nav-menus">
      <div class="menus">
        <i class='bx bxs-dashboard'></i><a href="">Dashboard</a>
      </div>

      <div class="menus">
        <i class='bx bx-file'></i><a href="">Request List</a>
      </div>

      <div class="menus">
        <i class='bx bx-cog' ></i><a href="">Tool Settings</a>
      </div>
    </div>
  </div>


<!-- MAIN CONTENT -->

  <div class="main-container">
    <h1>Dashboard</h1>

    <div style="width: 70%;  left: 26%; position: fixed; top: 18%; " class="table-data" >
      <div class="card">
        <Chart type="bar" :data="chartData" :options="chartOptions"  style="background-color: none;"    />
    </div>
    </div>
    

    <div class="transaction-history">
      <h2>Borrowed History</h2>
      <div class="data-table">
          <div class="colro">
            <table style="width:71%; position: fixed; left: 25%; border-radius: 5%;">
              <thead>
                <tr class="header">
                  <th>ID</th>
                  <th>Name</th>
                  <th>Equipment</th>
                  <th>Date</th>

                </tr>
              </thead>
              <tbody>
                <tr v-for="(transaction, index) in history" :key="index">
                  <td>{{ transaction.student_ID }}</td>
                  <td>{{ transaction.student_Name }}</td>
                  <td>{{ transaction.item_Name }}</td>
                  <td>{{ transaction.Borrow_Date_Time }}</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
    </div>
  </div>

  <div class="log-out">
    <RouterLink to="/login">
    <button >Sign Out</button><i class='bx bx-log-in'></i>
    </RouterLink>
  </div>

</template>


<script>
import { ref, onMounted } from "vue";
import axios from 'axios'; // Import axios for making HTTP requests
import Chart from 'primevue/chart';
import { ProductService } from '../services/ProductServices';
import DataTable from 'primevue/datatable';
import Column from 'primevue/column';
import { RouterLink } from "vue-router";

export default {
  setup() {
    const chartData = ref(null);
    const chartOptions = ref(null);
    const products = ref([]);
    const history = ref([]); // Define the reactive variable for history data

    // Function to fetch history data from the API
    const fetchHistoryData = async () => {
      try {
        const response = await axios.get("http://127.0.0.1:8000/api/student/student_list");
        history.value = response.data; // Update the history data with the response
      } catch (error) {
        console.error(error);
      }
    };

    onMounted(async () => {
      const data = await ProductService.getProductsMini();
      products.value = data;
      chartData.value = setChartData();
      chartOptions.value = setChartOptions();
      fetchHistoryData(); // Call the function to fetch history data when the component is mounted
    });

    const setChartData = () => {
      const documentStyle = getComputedStyle(document.documentElement);
      return {
        labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
        datasets: [
          {
            label: 'Most Borrowed Tool Set 1',
            backgroundColor: '#FF6C8B',
            borderColor: '#FF6C8B',
            data: [65, 59, 80, 81, 56, 55, 40]
          },
          {
            label: 'Most Borrowed Tool Set 2',
            backgroundColor: documentStyle.getPropertyValue('--gray-500'),
            borderColor: documentStyle.getPropertyValue('--gray-500'),
            data: [28, 48, 40, 19, 86, 27, 90]
          }
        ]
      };
    };

    const setChartOptions = () => {
      const documentStyle = getComputedStyle(document.documentElement);
      const textColor = documentStyle.getPropertyValue('--text-color');
      const textColorSecondary = documentStyle.getPropertyValue('--text-color-secondary');
      const surfaceBorder = documentStyle.getPropertyValue('--surface-border');

      return {
        maintainAspectRatio: false,
        aspectRatio: 0.8,
        plugins: {
          legend: {
            labels: {
              color: textColor
            }
          }
        },
        scales: {
          x: {
            ticks: {
              color: textColorSecondary,
              font: {
                weight: 500
              }
            },
            grid: {
              display: false,
              drawBorder: false
            }
          },
          y: {
            ticks: {
              color: textColorSecondary
            },
            grid: {
              color: surfaceBorder,
              drawBorder: false
            }
          }
        }
      };
    };

    return { chartData, chartOptions, products, history }; // Return the history data for use in the template
  },
  components: {
    Chart,
    DataTable,
    Column
  }
};



</script>

<style scoped>


/* Sign out  */

.log-out {
  position: fixed;
  margin-top: 20px;
  left: 90%;
}

.log-out button {
  border: none;
  background: none;
  font-size: 15px;
  
}

.log-out i {
 font-size: 18px;
 background: #CCCCCC;
 border-radius: 2px;
 width: 20px;
 color: #33363F;
}
/* TABLE EDITS */

table, td, th {  
    border: 2px solid #FB0664E0;
    background-color: #FFE3E7;
  }
  
  table {
    border-collapse: collapse;
    width: 50%;
    position: fixed;
    
  
  }
  
  th, td {
    padding: 15px;
  }
  th{
      background-color: #FFE3E7;
      border: 2px solid #FF6C8B;

  }


.main-container{
  position: fixed;
  height: 100%;
  width: 80%;
  left: 21%;
}

.p-chart {
  height: 17rem;
}

.transaction-history {

  top: 65%;
  position: fixed;
  height: 45%;
  width: 80%;
}

.p-datatable {
  position: fixed;
  left: 25%;
  width: 70%;
  box-shadow: 3px 5px  rgba(0, 0, 0, 0, 0.5);
  background-color: red !important;
}


.transaction-history h2 {
  font-size: 16px;
  left: 25%;
  top: 62%;
  position: fixed;
  font-family: 'Poppins', sans-serif;
  color: #8C0F3D;
}



































/* SIDE BAR SECTION! */

.side-bar {
  position: fixed;
  background-color: #FFF;
  height: 100%;
  width: 21%;
  border-right: 3px solid pink;
}

.logo-container {
  
  height: 20%;
  margin-top: 15%;
}

.logo-container img {
  position: fixed;
  width: 14%;
  left: 3%;
  
}

.nav-menus {
  position: fixed;
  margin-top: 8%;
  width: 20.9%;

}

.menus  {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 5%;
    height: 80px;
   

}

.menus:active,
.menus:focus
.menus a:focus {
  border: 2px solid #FF6C8B;
  background-color: #FFCBD5;
  border-right: 5px solid #FF6C88;
  color: white; /* Adjust text color for better visibility */
}

.menus a {
    text-decoration: none;
    color: black; /* Adjust the color as needed */
    display: flex;
    justify-content: center;
    align-items: center;
    width: 45%; /* Make sure the anchor takes full width */
    height: 100%; /* Make sure the anchor takes full height */
    font-size: 20px;
    font-weight: 200;
    font-family: 'Poppins', sans-serif;

  }

  .menus i {
    font-size: 2rem;
    background: #CCCCCC;
    height: 33px;
    width: 33px;
    border-radius: 7px;
  }



</style>