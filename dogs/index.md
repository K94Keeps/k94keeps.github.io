---
layout: default
title: Adoptable Dogs
---
<div class="container">
  <h1>{{ page.title }}</h1>
  <div class="row">
    <div class="col-md-12">
      <p>Find out more about our adoption process and fill out an applicaiton, <a href="/adopt/">here</a>.</p>
    </div>
  </div>
  <br />
  <div id='doglist' class="row">
    <h2 id='loading' class='text-center'>Fetching pups...</h2>
    <h2 id='fail' class='text-center' style='display: none;'>Failed to fetch pups!</h2>
  </div><!-- /.row -->
</div><!-- /.container -->

<script>
$.getJSON('https://api.petfinder.com/shelter.getPets?format=json&key=834f77ab998a9623d5abbc5c71cf908b&callback=?&id=IL759')
  .done(function(data) {
    const pets = data.petfinder.pets.pet.sort((a, b) => a.name.$t.localeCompare(b.name.$t));
    for (const pet of pets) {
      const template = `
        <div class="col-md-4 text-center">
          <a href='/dogs/view?id=${pet.id.$t}'><img class="img-circle hover-zoom" src="http://photos.petfinder.com/photos/pets/${pet.id.$t}/1/" alt="${pet.name.$t}" width="140" height="140" style='object-fit: cover'></a>
          <h2>${pet.name.$t}</h2>
          <p>
            ${pet.sex.$t === 'F' ? 'Female' : 'Male'}<br />
            ${pet.breeds.breed.length ? pet.breeds.breed.map((a) => a.$t).join(', ') : pet.breeds.breed.$t}<br />
            ${pet.age.$t}
          </p>
          <p><a class="btn btn-default" href="/dogs/view?id=${pet.id.$t}" role="button">More details &raquo;</a></p>
        </div><!-- /.col-md-4 -->
      `
      $(template).appendTo($('#doglist'));
    }
	})
  .fail(() => { $('#fail').show(); })
  .always(() => { $('#loading').hide(); });

</script>
