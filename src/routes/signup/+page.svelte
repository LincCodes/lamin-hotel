<script>

    import { supabase } from '../supabaseClient'
    import {goto} from '$app/navigation';
    
        
        let hide = true;
        let err = '';
    
        // @ts-ignore
    async function signup(e) {
        const email = e.target.email.value;
        const password = e.target.password.value;
        const pass = e.target.pass.value;
        const name = e.target.name.value;
        const phone = e.target.phone.value;
        const address = e.target.address.value;
        const gender = e.target.gender.value;
        console.log(name, phone, address, gender);

        
        if(password==pass){
            const { user, error } = await supabase.auth.signUp({email,password})
            console.log("user",user);
            console.log("error",error);
            if (error) {
                hide = false;
                err = error.message;
            } else {
                const { data, error } = await supabase
                .from('guest')
                .insert([
                    // @ts-ignore
                    { guest_id: user.id,gender:gender, phone_no: phone, email: email, address: address, full_name: name }
                ])
                if (data) {
                    goto("/")
                } else {
                    hide = false;
                    err = error.message;
                    console.log(error)
                }
            }
        }
        
    }
</script>

<section class="text-light position-relative py-4 py-xl-5" style="background-image: url(back.jpg);background-position: top center;">
    <div class="container">
        <div class="row mb-5">
            <div class="col-md-8 col-xl-6 text-center mx-auto">
                <h2>Sign Up</h2>
                <p class="w-lg-50">Create a new account</p>
            </div>
        </div>
        <div class="row d-flex justify-content-center">
            <div class="col-md-6 col-xl-4">
                <div class="card mb-5">
                    <div class="card-body d-flex flex-column align-items-center">
                        <div class="bs-icon-xl bs-icon-circle bs-icon-primary bs-icon my-4"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" fill="currentColor" viewBox="0 0 16 16" class="bi bi-person">
                                <path d="M8 8a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm2-3a2 2 0 1 1-4 0 2 2 0 0 1 4 0zm4 8c0 1-1 1-1 1H3s-1 0-1-1 1-4 6-4 6 3 6 4zm-1-.004c-.001-.246-.154-.986-.832-1.664C11.516 10.68 10.289 10 8 10c-2.29 0-3.516.68-4.168 1.332-.678.678-.83 1.418-.832 1.664h10z"></path>
                            </svg></div>
                        
                        <div class="alert alert-success text-bg-warning" class:hide role="alert"><span>{err}<br></span></div>
                        <form class="text-center" on:submit|preventDefault={signup}>
                            <div class="mb-3"><input class="form-control" type="text" name="name" placeholder="Full Name" required></div>
                            <div class="mb-3"><input class="form-control" type="email" name="email" placeholder="Email" required></div>
                            <div class="mb-3"><input class="form-control" type="tel" name="phone" placeholder="Enter phone" required></div>
                            <div class="mb-3"><input class="form-control" type="text" name="address" placeholder="Adress" required></div>
                            <div class="mb-3">
                                <select class="form-select" name="gender" id="gender">
                                    <optgroup label="Select a gender">
                                        <option value="Female">Female</option>
                                        <option value="Male">Male</option>
                                    </optgroup>
                                </select>
                            </div>
                            <div class="mb-3"><input class="form-control" type="password" name="password" placeholder="Password" required></div>
                            <div class="mb-3"><input class="form-control" type="password" name="pass" placeholder="Confirm Password" required></div>
                            <div class="mb-3"><button class="btn btn-primary d-block w-100" type="submit">Sign Up</button></div>
                            <p class="text-muted">Create a new account</p>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</section>

<style>
    .hide{
        display: none;
    }
</style>