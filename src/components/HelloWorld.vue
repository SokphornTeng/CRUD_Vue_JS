<template>
  <div id="app">
    <h2 class="text-center mt-4 mb-4">Application</h2>
    <div class="container-fluid">
        <div class="table-responsive">
          <button v-b-modal.modal-prevent-closing  class="btn btn-success" style="float: left;">Create +</button>
            <table class="table" v-show="persons.length">
                <thead class="thead-dark">
                    <tr>
                        <th v-for="column in thList" :key="column.id">{{column}}</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(person,index) in persons" :key="index">
                        <td class="text-center">{{index + 1}}</td>
                        <td>
                            {{person.lname}}
                        </td>
                        <td>
                            {{person.fname}}
                        </td>
                        <td>
                            {{person.age}} years
                        </td>
                        <td>
                            {{person.job}}
                        </td>
                        <td>
                            {{person.address}}
                        </td>
                        <td>
                            <div style="width:150px;">
                                <a href="#"  class="btn btn-warning" v-b-modal.modal-edit @click="editInfo(index)">Edit</a> /
                                <a href="#" class="btn btn-danger" @click="deleteInfo(index)">Delete</a>
                            </div>
                        </td>
                    </tr>
                  
                </tbody>
            </table>
        </div>
    </div>


    <!-- Create Model -->
    <b-modal
      id="modal-prevent-closing"
      ref="modal"
      title="Create Data"
    >
        <form >
                            <div class="input-field ">
                              <label for="last_name">Last Name</label>
                                <input placeholder="Last Name" id="last_name" type="text" v-model="listInfo.lname" >
                            </div>
                            <div class="input-field ">
                              <label for="first_name">First Name</label>
                                <input placeholder="Frist Name" id="first_name" type="text" v-model="listInfo.fname" >
                              </div>
                            <div class="input-field ">
                              <label for="edit_age">Age</label>
                                <input placeholder="Age" id="edit_age" type="text" v-model="listInfo.age" >
                                </div>
                            <div class="input-field ">
                              <label for="edit_job">Job</label>
                                <input placeholder="Job" id="edit_job" type="text" v-model="listInfo.job">
                            </div>
                            <div class="input-field">
                              <label for="edit_address">Address</label>
                                <input placeholder="Address" id="edit_address" type="text" v-model="listInfo.address">
                            </div>
                    </form>
                    <div class="modal-footer">
                    <button type="button" class="btn btn-primary" @click="addInfo()">Create</button>
                </div>
    </b-modal>

       <!-- Edit Model -->
       <b-modal
      id="modal-edit"
      ref="modal"
      title="Create Data"
    >
    <form >
                            <div class="input-field ">
                              <label for="last_name">Last Name</label>
                                <input placeholder="Last Name" id="last_name" type="text" v-model="editInput.lname" >
                            </div>
                            <div class="input-field ">
                              <label for="first_name">First Name</label>
                                <input placeholder="Frist Name" id="first_name" type="text" v-model="editInput.fname" >
                              </div>
                            <div class="input-field ">
                              <label for="edit_age">Age</label>
                                <input placeholder="Age" id="edit_age" type="text" v-model="editInput.age" >
                                </div>
                            <div class="input-field ">
                              <label for="edit_job">Job</label>
                                <input placeholder="Job" id="edit_job" type="text" v-model="editInput.job">
                            </div>
                            <div class="input-field">
                              <label for="edit_address">Address</label>
                                <input placeholder="Address" id="edit_address" type="text" v-model="editInput.address">
                            </div>
                    </form>
                      <div class="modal-footer">
                    <button type="button" class="btn btn-primary" @click="updateInfo()">Save Edit</button>
                </div>
    </b-modal>
    </div>
</template>
<script>
import  axios  from 'axios'
export default {
  name: 'HelloWorld',
  data() {
     return {
       thList: [
       "ID",
      "Last Name",
      "First Name",
      "Age",
      "Job",
      "Address",
      "Actions "
       ],
       persons: [
       {
        lname: "ADIASSA",
        fname: "Ethiel",
        age: 20,
        job: "Web Developer",
        address: "Lome-Togo"
      },
      {
        lname: "ADUFU",
        fname: "Patrick",
        age: 20,
        job: "Banker",
        address: "Senegal-Dakar"
      },
      {
        lname: "MOUTON",
        fname: "John",
        age: 28,
        job: "Scientist",
        address: "New-York/USA"
      },
      {
        lname: "SMITH",
        fname: "Luther",
        age: 18,
        job: "Pilot",
        address: "London/GB"
      },
      {
        lname: "WALTER",
        fname: "Ramses Peter",
        age: 38,
        job: "Doctor",
        address: "Paris/France"
      },
      {
        lname: "GEORGES",
        fname: "Luther",
        age: 45,
        job: "Musician",
        address: "Vienne"
      },
      {
        lname: "MICHAEL",
        fname: "Daven",
        age: 27,
        job: "Boxer",
        address: "Pekin/China"
      }
       ],
       listInfo: {
        lname: '',
        fname: '',
        age: 0,
        job: '',
        address: ''
       },
       editInput: {
        lname: '',
        fname: '',
        age: 0,
        job: '',
        address: ''
       },
       showModal: false,
       indexEdit: 0
     }
  },
  methods: {
     addInfo() {
       this.persons.push({
        lname: this.listInfo.lname,
        fname: this.listInfo.fname,
        age: this.listInfo.age,
        job: this.listInfo.job,
        address: this.listInfo.address
       })
       for(var i in this.listInfo){
        this.listInfo[i] = '';
       }
       this.showModal = !this.showModal;
      //  this.persons.sort(ordonner);
      //  this.$refs.lname.focus()
     },
     editInfo(index){
      this.editInput.lname = this.persons[index].lname,
      this.editInput.fname = this.persons[index].fname,
      this.editInput.age = this.persons[index].age,
      this.editInput.job = this.persons[index].job,
      this.editInput.address = this.persons[index].address;
      this.indexEdit = index;
     },
     updateInfo(){
      this.persons.splice(this.indexEdit, 1);
      this.persons.push({
        lname: this.editInput.lname,
        fname: this.editInput.fname,
        age: this.editInput.age,
        job: this.editInput.job,
        address: this.editInput.address
      });
      for(var j in this.editInput){
        this.editInput[j] = "";
      }
     },
     deleteInfo(index){
       this.persons.splice(index, 1)
     }
  },
  created() {
    this.addInfo();
  }
}
</script>
