<template>
  <div>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">Fisrst Name</th>
          <th scope="col">Last Name</th>
          <th scope="col">Email</th>
          <th scope="col">Phone</th>
          <th scope="col">Actions</th>
        </tr>
      </thead>
      <tbody v-for="(customer, index) in customers" :key="index">
        <tr>
          <td>{{ customer.firstName }}</td>
          <td>{{ customer.LastName }}</td>
          <td>{{ customer.email }}</td>
          <td>{{ customer.phone }}</td>
          <td>
            <a :href="'/customer' + customer.id" class="btn btn-primary">
              Edit
            </a>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import CustomerDataService from "@/services/CustomerDataService";

export default {
  /* eslint-disable */
  name: "customers",
  data() {
    return {
      customers: [],
    };
  },
  methods: {
    retrieveCustomers() {
      // axios로 spring에 모든 회원 조회 요청
      CustomerDataService.getAll()
        // 성공하면 then으로 서버(spring) 데이터(response.data)가 들어옴
        .then((response) => {
          this.customers = response.data;
        })
        // 실패하면 catch로 에러메시지가 들어옴
        .catch((e) => {
          alert(e);
        });
    },
  },
  // 화면이 뜨자마자 실행되는 이벤트 (모든 회원조회가 실행됨)
  mounted() {
    this.retrieveCustomers();
  },
};
</script>

<style scoped></style>
