---
layout: default
custom_css:
 - /css/dog.css
---
<div id='target' class="container">
    <h2 id='loading' class='text-center'>Fetching pup...</h2>
    <h2 id='fail' class='text-center' style='display: none;'>Couldn't fetch pup!</h2>
</div><!-- /.container -->

<script>

function fail() {
  $('#fail').show();
}

const params = new URLSearchParams(window.location.search);
const id = params.get('id');
if (!id) {
  fail();
}

const client_id = 'MPK3ETCiXDCUNQY4rVSGEfQFssitKMUxDn9ecWiIdbZJ9MQUWE';
const client_secret = 'JUZJIYvmUwvjxh6lDF9KZfZRyF7gsVwWs22TkVGJ';
const post_data = `grant_type=client_credentials&client_id=${client_id}&client_secret=${client_secret}`;
$.post('https://api.petfinder.com/v2/oauth2/token', post_data)
  .then(function(tokenResponse) {
    return $.ajax({
      url: `https://api.petfinder.com/v2/animals/${id}`,
      dataType: 'json',
      headers: {
        'Authorization': `Bearer ${tokenResponse.access_token}`,
      },
    });
  })
  .done(function(data) {
    const pet = data.animal;
    const pics = pet.photos.map(photo => photo.full);
    const available = pet.status === 'adoptable';
    const title = available ? `Meet ${pet.name}` : `${pet.name} is adopted!`;
    const adoptButton = available ? `
            <div class="clearfix">
              <p class="pull-right"><a class="btn btn-success" href="/adopt/">Adopt ${pet.name}</a></p>
            </div>` : '';

    let carousel = `
          <div id='carousel-dog' class='carousel slide'>
            <div class='carousel-inner'>
    `;

    let first = true;
    for (const pic of pics) {
      const activeClass = first ? 'active' : '';
      first = false;
      carousel += `
                <div class="item ${activeClass}">
                  <img src='${pic}' alt='' style='object-fit: cover;'/>
                </div>`;
    }
    carousel += `
            </div>
          </div>
          <div class="thumbs clearfix">
          `;
    let index = 0;
    for (const pic of pics) {
      const activeClass = index === 0 ? 'active' : '';
      carousel += `
              <div data-target='#carousel-dog' data-slide-to='${index}' class="item ${activeClass}"><a href=#"><img class="thumb img-thumbnail" src='${pic}' alt='' /></a></div>
      `;
      index++;
    }

    carousel += `
          </div>
    `;


    const template = `
      <h1>${title}</h1>
      <div class="row">
        <div id='carousel' class="col-lg-5">
          <!-- carousel -->
        </div>
        <div class="col-lg-7">
          <p>${pet.description}</p>
          <br />
            <div class="clearfix">
              <p class="pull-right"><a class="btn btn-info" href="https://www.petfinder.com/petdetail/${pet.id}" target="_blank">See ${pet.name} on Petfinder</a></p>
            </div>
            ${adoptButton}
          <br />
          <div class="alert alert-info">
            <p>All K9 4 KEEPS dogs are up to date on all vaccinations and are spayed/neutered, heartworm tested and microchipped by the time an adoption is finalized. (Puppies may not have their entire set of shots.)</p>
          </div>
        </div>
      </div>
    `;
    $(template).appendTo($('#target'));
    $(carousel).appendTo($('#carousel'));
	})
  .fail(() => { fail(); })
  .always(() => { $('#loading').hide(); });

</script>

