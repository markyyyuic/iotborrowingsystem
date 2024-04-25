<template>
    <div>
      <navbar/>
      <div class="main">
        <div class="wrapper">
          <p class="name">MARC COSTILLAS</p>
          <p class="section">BSIT - 2A</p>
          <p class="subject">CC112</p>
        </div>
  
        <div class="data-table">
          <div class="colro">
            <table style="width:100%">
              <thead>
                <tr class="header">
                  <th>ID Number</th>
                  <th>Student</th>
                  <th>Log In Time</th>
                  <th>Log Out Time</th>
                  <th>Status</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(student, index) in attendance" :key="index">
                  <td>{{ student.student_id }}</td>
                  <td>{{ student.student_name }}</td>
                  <td>{{ student.log_in }}</td>
                  <td>{{ student.log_out }}</td>
                  <td>{{ student.status }}</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </template>
    
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import axios from 'axios';
  import navbar from "../components/navbar.vue";
  
  const attendance = ref([]);
  
  const fetchAttendance = async () => {
    try {
      const response = await axios.get("http://127.0.0.1:8000/api/student");
      attendance.value = response.data;
    } catch (error) {
      console.error(error);
    }
  };
  
  onMounted(() => {
    fetchAttendance();
  });
  </script>
  
  <style> 
  html {
      height: 100%;
      width: 100%
  }
  
  table, td, th {  
    border: 1px solid #FB0664E0;
  }
  
  table {
    border-collapse: collapse;
    width: 100%;
  }
  
  th, td {
    padding: 15px;
  }
  th{
      background-color: #FB0664E0;
      border-right: 1px solid white;
      border-left: 1px solid white;
  }
  
  .wrapper{
      box-shadow: 5px 5px 6px #000000;
      background-color:rgb(254, 254, 254);
      height: 200px;
      width: 1450px;
      position: fixed;
      top: 50px;
      margin-left: 400px;
      border-radius: 15px;
  }
  
  .main .wrapper .name{
      position: relative;
      left: -480px;
      top: -25px;
      font-weight: bolder;
      font-size: 45px;
  }
  
  .main .wrapper .section{
      position: relative;
      left: -612px;
      top: -10px;
      font-weight: 400;
      font-size: 35px;
  }
  
  .main .wrapper .subject{
      position: relative;
      left: 580px;
      top: -210px;
      font-weight: 400;
      font-size: 45px;
  }
  
  .main .data-table{
      width: 1450px;
      height: 70px;
      position: relative;
      left: 400px;
      top: 270px;
      background-color: none;
      border-radius: 25px;
      font-family: Verdana, Geneva, Tahoma, sans-serif;
      color: white;
      font-weight: bold;
  }
  
  .main .data-table .colro table{
      position: relative;
      left: 5px;
      top: 10px;
  
  }
  
  .main .data-table .colro .Present{
      background-color: #86D63D;
      border-radius: 30px;
  }
  
  .main .data-table .colro .Absent{
      background-color: #F70202;
      border-radius: 30px;
  }
  
  .main .data-table .colro .Excused{
      background-color: #726363;
      border-radius: 30px;
  }
  
  .dropbtn {
      
      font-family: Verdana, Geneva, Tahoma, sans-serif;
      color: white;
      font-weight: bold;
      border: none;
  }
  
  .dropdown {
    position: relative;
    display: inline-block;
  }
  
  .dropdown-content {
      background-color: white;
      border: 1px solid black;
      border-radius: 15px;
      display: none;
      position: absolute;
      min-width: 200px;
      box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
  }
  
  .dropdown-content a {
      position: relative;
      left: 25px;
      width: 150px;
      color: black;
      padding: 12px 10px;
      text-decoration: none;
      display: block;
      -webkit-transition: all 0.3s ease;
      -moz-transition: all 0.3s ease;
      -ms-transition: all 0.3s ease;
      transition: all 0.3s ease;
  }
  
  .dropdown-content a:hover {
      padding: 15px 13px;
      border: 1px solid black;
  
  }
  
  .dropdown:hover .dropdown-content {display: block;}
  
  i{
      position: relative;
      left: -15px;
  }
  
  i{
      position: relative;
      left: -15px;
  }
  
  
  
  
  
  
  
  @media screen and (max-height: 450px) {
    .sidenav {padding-top: 15px;}
    .sidenav a {font-size: 18px;}
  }
  </style>