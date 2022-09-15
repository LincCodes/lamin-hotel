<script>

    import { supabase } from './supabaseClient'
    import {goto} from '$app/navigation';
    import { v4 as uuidv4 } from 'uuid';
    
        
    let hide = true;
    let err = '';
    
        // @ts-ignore
    async function send(e) {
        const booking_date = e.target.booking_date.value;
        const room_type = e.target.room_type.value;
        const adults = e.target.adults.value;
        const children = e.target.children.value;
        const departure_date = e.target.departure_date.value;
        const arrival_date = e.target.arrival_date.value;
        const booking_id = uuidv4();
        const hotel_id = "Lamin";
        const room_no = Math.floor(Math.random() * 10) + 1;
        console.log(booking_date, room_type, adults, children, arrival_date, departure_date, booking_id, hotel_id, room_no);

        
        const { data, error } = await supabase
        .from('booking')
        .insert([
            // @ts-ignore
            { booking_date, room_type, adults, children, arrival_date, departure_date, booking_id, hotel_id, room_no }
        ])
        if (data) {
            console.log(data)
            hide = false;
            err = "Booked!";
        } else {
            hide = false;
            err = error.message;
            console.log(error)
        }
        
    }
</script>


<nav class="navbar navbar-dark navbar-expand-lg fixed-top bg-dark" id="mainNav">
    <div class="container"><a class="navbar-brand" href="index.html">Lamin Hotel</a><button data-bs-toggle="collapse" data-bs-target="#navbarResponsive" class="navbar-toggler navbar-toggler-right" type="button" aria-controls="navbarResponsive" aria-expanded="false" aria-label="Toggle navigation"><i class="fa fa-bars"></i></button>
        <div class="collapse navbar-collapse" id="navbarResponsive">
            <ul class="navbar-nav ms-auto text-uppercase">
                <li class="nav-item"><a class="nav-link active" href="index.html">HOME</a></li>
                <li class="nav-item"><a class="nav-link" href="#rooms">ROOMS</a></li>
                <li class="nav-item"><a class="nav-link" href="#photos">PHOTOS</a></li>
                <li class="nav-item"><a class="nav-link" href="#">ABOUT</a></li>
                <li class="nav-item"><a class="nav-link" href="#">Contact</a></li>
            </ul><a href="/login" class="btn btn-link" type="button" style="margin-right: 10px;">LOGIN</a><a href="/signup" class="btn btn-primary" type="button">SIGNUP</a>
        </div>
    </div>
</nav>
<header class="masthead" style="background-image:url('back.jpg');background-position:top center;">
    <div class="container">
        <div class="intro-text">
            <div class="intro-lead-in"><span><strong>Welcome To Lamin Hotel Online Booking!</strong></span></div>
            <div class="intro-heading text-uppercase"><span>Providing the best of services</span></div><a class="btn btn-primary btn-xl text-uppercase" role="button" href="#book">BOOK NOW!</a>
        </div>
    </div>
</header>
<section id="rooms" class="article-list" style="padding: 50px 0;">
    <div class="container">
        <div class="intro">
            <h1 class="text-center">ROOMS</h1>
            <p class="text-center">Check out our rooms and their corresponding pricing</p>
        </div>
        <div class="row articles" style="padding: 0;">
            <div class="col-sm-6 col-md-4 item"><a href="#"><img class="img-fluid" src="single.jpg"></a>
                <h3 class="name">Single</h3>
                <p class="description">K400</p>
            </div>
            <div class="col-sm-6 col-md-4 item"><a href="#"><img class="img-fluid" src="fam.jpg"></a>
                <h3 class="name">Family</h3>
                <p class="description">K750</p>
            </div>
            <div class="col-sm-6 col-md-4 item"><a href="#"><img class="img-fluid" src="pres.jpg"></a>
                <h3 class="name">Presidential</h3>
                <p class="description">K1200</p>
            </div>
        </div>
    </div>
</section>
<div class="container" id="photos" style="padding: 0;padding-bottom: 50px;">
    <h1 class="text-center">Photos</h1>
    <div class="simple-slider" style="padding-top: 20px;">
        <div class="swiper-container">
            <div class="swiper-wrapper">
                <div class="swiper-slide" style="background: url(1.jpg) center center / cover no-repeat;"></div>
                <div class="swiper-slide" style="background: url(2.jpg) center center / cover no-repeat;"></div>
                <div class="swiper-slide" style="background: url(3.jpg) center center / cover no-repeat;"></div>
            </div>
            <div class="swiper-pagination"></div>
            <div class="swiper-button-prev"></div>
            <div class="swiper-button-next"></div>
        </div>
    </div>
</div>
<section id="book" class="contact-clean">
    <form method="post" on:submit|preventDefault={send}>
        <h2 class="text-center">Make a Reservation</h2>
        <div class="alert alert-success text-bg-warning" class:hide role="alert"><span>{err}<br></span></div>
        <div class="mb-3"><label class="form-label">Adults:</label><input class="form-control" type="number" name="adults" placeholder="0" value="0" min="0" required></div>
        <div class="mb-3"><label class="form-label">Children:</label><input class="form-control" type="number" name="children" placeholder="0" value="0" min="0" required></div>
        <div class="mb-3">
            <select class="form-select" name="room_type" id="room_type">
                <optgroup label="Select a room type:">
                    <option value="Personal">Personal</option>
                    <option value="Family">Family</option>
                    <option value="Presidential">Presidential</option>
                </optgroup>
            </select>
        </div>
        <div class="mb-3"><label class="form-label">Booking Date:</label><input class="form-control" type="date" name="booking_date" required></div>
        <div class="mb-3"><label class="form-label">Arrival Date:</label><input class="form-control" type="date" name="arrival_date" required></div>
        <div class="mb-3"><label class="form-label">Departure Date:</label><input class="form-control" type="date" name="departure_date" required></div>
        <div class="mb-3"><button class="btn btn-primary" type="submit">send </button></div>
    </form>
</section>
<footer class="footer-basic">
    <div class="social"><a href="#"><i class="icon ion-social-whatsapp"></i></a><a href="#"><i class="icon ion-social-twitter"></i></a><a href="#"><i class="icon ion-social-facebook"></i></a></div>
    <ul class="list-inline">
        <li class="list-inline-item"><a href="#">Home</a></li>
        <li class="list-inline-item"><a href="#rooms">Rooms</a></li>
        <li class="list-inline-item"><a href="#photos">Photos</a></li>
        <li class="list-inline-item"><a href="#">About</a></li>
        <li class="list-inline-item"><a href="#">Contact</a></li>
    </ul>
    <p class="copyright">Lamin Hotel © 2022</p>
</footer>


<style>
    .hide{
        display: none;
    }
</style>