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
const client_id = 'MPK3ETCiXDCUNQY4rVSGEfQFssitKMUxDn9ecWiIdbZJ9MQUWE';
const client_secret = 'JUZJIYvmUwvjxh6lDF9KZfZRyF7gsVwWs22TkVGJ';
const post_data = `grant_type=client_credentials&client_id=${client_id}&client_secret=${client_secret}`;
$.post('https://api.petfinder.com/v2/oauth2/token', post_data)
  .then(function(tokenResponse) {
    return $.ajax({
      url: 'https://api.petfinder.com/v2/animals?organization=IL759&limit=100&status=adoptable',
      dataType: 'json',
      headers: {
        'Authorization': `Bearer ${tokenResponse.access_token}`,
      },
    });
  })
  .done(function(data) {
    const pets = data.animals.sort((a, b) => a.name.localeCompare(b.name));
    for (const pet of pets) {
      const template = `
        <div class="col-md-4 text-center">
          <a href='/dogs/view?id=${pet.id}'><img class="img-circle hover-zoom" src="${pet.photos[0].medium}" alt="${pet.name}" width="140" height="140" style='object-fit: cover'></a>
          <h2>${pet.name}</h2>
          <p>
            ${pet.gender}<br />
            ${[pet.breeds.primary, pet.breeds.secondary].filter(a => a).join(', ')}<br />
            ${pet.age}
          </p>
          <p><a class="btn btn-default" href="/dogs/view?id=${pet.id}" role="button">More details &raquo;</a></p>
        </div><!-- /.col-md-4 -->
      `
      $(template).appendTo($('#doglist'));
    }
	})
  .fail(() => { $('#fail').show(); })
  .always(() => { $('#loading').hide(); });

</script>
