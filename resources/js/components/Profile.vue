<style>
.widget-user-header {
    background-position: center center;
    background-size: cover;
    height: 200px;
}

.widget-user .card-footer {
    padding-top: 10px;
    padding-bottom: 5px;
}
</style>


<template>
    <div class="container">
        <div class="row">
            <div class="col-md-12 mt-3">

                <div class="card card-widget widget-user">
                <!-- Add the bg color to the header using any of the bg-* classes -->
                    <div class="widget-user-header text-white" style="background: url('./img/the_sun.jpg')">
                        <h3 class="widget-user-username">Elizabeth Pierce</h3>
                        <h5 class="widget-user-desc">Web Designer</h5>
                    </div>
                    <div class="widget-user-image">
                        <img class="img-circle" src="" alt="User Avatar">
                    </div>
                    <div class="card-footer">
                        <div class="row">
                            <div class="col-sm-4 border-right">
                                <div class="description-block">
                                    <h5 class="description-header">3,200</h5>
                                    <span class="description-text">SALES</span>
                                </div>
                            <!-- /.description-block -->
                            </div>
                            <!-- /.col -->
                            <div class="col-sm-4 border-right">
                                <div class="description-block">
                                    <h5 class="description-header">13,000</h5>
                                    <span class="description-text">FOLLOWERS</span>
                                </div>
                            <!-- /.description-block -->
                            </div>
                            <!-- /.col -->
                            <div class="col-sm-4">
                                <div class="description-block">
                                    <h5 class="description-header">35</h5>
                                    <span class="description-text">PRODUCTS</span>
                                </div>
                            <!-- /.description-block -->
                            </div>
                        <!-- /.col -->
                        </div>
                    <!-- /.row -->
                    </div>
                </div>


            </div>
<!-- toda la parte de arriba -->

<!-- empieza toda la parte de abajo -->
<div class="col-md-12 mt-3">
            <div class="card">
              <div class="card-header p-2">
                <ul class="nav nav-pills">
                  <li class="nav-item"><a class="nav-link active show" href="#activity" data-toggle="tab">Activity</a></li>
                  
                  <li class="nav-item"><a class="nav-link" href="#settings" data-toggle="tab">Settings</a></li>
                </ul>
              </div><!-- /.card-header -->
              <div class="card-body">
                <div class="tab-content">
                  <div class="tab-pane active show" id="activity">
                    <!-- Post -->
                    
                    <!-- /.post -->
                  </div>
                  
                  <!-- /.tab-pane -->

                  <div class="tab-pane" id="settings">
                    <form class="form-horizontal">
                      <div class="form-group">
                        <label for="inputName" class="col-sm-2 control-label">Nombre</label>

                        <div class="col-sm-10">
                          <input type="text" v-model="form.name" class="form-control" id="inputName" placeholder="Name">
                        </div>
                      </div>
                      <div class="form-group">
                        <label for="inputEmail" class="col-sm-2 control-label">Email</label>

                        <div class="col-sm-10">
                          <input type="email" v-model="form.email" class="form-control" id="inputEmail" placeholder="Email">
                        </div>
                      </div>
                      
                      <div class="form-group">
                        <label for="inputExperience" class="col-sm-2 control-label">Experiencia</label>

                        <div class="col-sm-10">
                          <textarea class="form-control" id="inputExperience" placeholder="Experience"></textarea>
                        </div>
                      </div>

                      <div class="form-group">
                        <label for="photo" class="col-sm-2 control-label">Profile Photo</label>
                            <div class="col-sm-12">
                              <input type="file" @change="updateProfile" class="form-input" name="photo">
                              
                            </div>
                        
                      </div>

                      <div class="form-group">
                        <label for="inputEmail" class="col-sm-12 control-label">Passport (si no se cambia dejar en blanco)</label>

                        <div class="col-sm-10">
                          <input type="email" class="form-control" id="inputEmail" placeholder="Passport">
                        </div>
                      </div>
                      <div class="form-group">
                        <div class="col-sm-offset-2 col-sm-10">
                          <button @click.prevent="updateInfo" type="submit" class="btn btn-success">Update</button>
                        </div>
                      </div>
                    </form>
                  </div>
                  <!-- /.tab-pane -->
                </div>
                <!-- /.tab-content -->
              </div><!-- /.card-body -->
            </div>
            <!-- /.nav-tabs-custom -->
          </div>


        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                form: new Form({
                    id: '',
                    name: '',
                    email: '',
                    password: '',
                    type: '',
                    bio: '',
                    photo: ''
                })
            }
        },

        mounted() {
            console.log('Component mounted.')
        },

        methods:{
          updateInfo() {
              this.$Progress.start();

              this.form.put('api/profile/')
              .then(() => {

                this.$Progress.finish();

              })
              .catch(() => {

                this.$Progress.fail();

              });
          },

          updateProfile(e){
            //console.log('subiendo foto');
              let file = e.target.files[0];
              //console.log(file);
              let reader = new FileReader();

              if(file['size'] < 2111775){
                reader.onloadend = (file) => {
                //console.log('RESULT', reader.result);
                this.form.photo = reader.result;
                }
                reader.readAsDataURL(file);
              }else{
                Swal.fire({
                    title: 'Oops...',
                    text: "No puede subir un archivo tan grande!",
                    type: 'error',
                    
                })


              }
              
          }
        },

        created() {
            axios.get("api/profile").then(({ data }) => (this.form.fill(data)));
        }
    }
</script>