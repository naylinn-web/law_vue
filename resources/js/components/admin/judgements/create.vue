<template>
    <div>
        <!-- Content Header (Page header) -->
        <div class="content-header">
            <div class="container-fluid">
                <div class="row mb-2">
                    <div class="col-sm-6">
                        <h1 class="m-0 text-dark">New Judgement</h1>
                    </div><!-- /.col -->
                    <div class="col-sm-6">
                        <ol class="breadcrumb float-sm-right">
                            <router-link to="/judgements" class="btn btn-sm btn-primary">
                               <i class="fa fa-arrow-circle-left"></i>&nbsp;&nbsp;Back</router-link>
                        </ol>
                    </div><!-- /.col -->
                </div><!-- /.row -->
            </div><!-- /.container-fluid -->
        </div>
        <!-- /.content-header -->

        <!-- Main content -->
        <div class="content">
            <div class="container-fluid">
                <div class="row">
                    <div class="col-lg-12">
                        <div class="card card-info">
                            <div class="card-header">
                                <h3 class="card-title">New Judgement Form</h3>
                            </div>
                            <!-- /.card-header -->
                            <!-- form start -->
                            <form class="form-horizontal" @submit.prevent="onSubmit" @keydown="form.errors.clear()">
                                <div class="card-body" style="height: 239px;">
                                    <div class="form-group row">
                                        <label for="title" class="col-sm-2 col-form-label">Title</label>
                                        <div class="col-sm-10">
                                            <input type="text" class="form-control" id="title" name="title" autocomplete="title" autofocus placeholder="Title" v-model="form.title">
                                            <span class="invalid-feedback d-block" role="alert" v-if="form.errors.has('title')" v-text="form.errors.get('title')"></span>
                                        </div>
                                    </div>
                                    <div class="form-group row">
                                        <label for="inputEmail3" class="col-sm-2 col-form-label">Description</label>
                                        <div class="col-sm-10">
                                            <textarea class="form-control" name="descripion" v-model="form.description"></textarea>
                                            <span class="invalid-feedback d-block" role="alert" v-if="form.errors.has('description')" v-text="form.errors.get('description')"></span>
                                        </div>
                                    </div>
                                </div>
                                <!-- /.card-body -->
                                <div class="card-footer">
                                    <button type="submit" class="btn btn-info" :disabled="form.errors.any()">Save</button>
                                </div>
                                <!-- /.card-footer -->
                            </form>
                        </div>
                    </div>
                </div>
            </div>
            <!-- /.container-fluid -->
        </div>
        <!-- /.content -->

    </div>

</template>

<script>
    export default {
            data() {
                return {
                    user: {},
                    form: new Form({
                        'title': '',
                        'description': ''
                    })
                }
            },
            methods: {
                onSubmit() {
                    this.form
                        .post('http://law.test/api/judgement/store', this.user)
                        .then((response) => {
                            Toast.fire({
                                icon: 'success',
                                title: 'Judgement created successfully'
                            })
                            this.$router.push({name: 'judgements'})
                        })
                        .catch(error => console.log(error))
                        .finally(() => this.loading = false)
                }
            }
        }

</script>
