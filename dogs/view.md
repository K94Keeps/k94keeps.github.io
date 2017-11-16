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

const url = `https://api.petfinder.com/pet.get?format=json&key=834f77ab998a9623d5abbc5c71cf908b&callback=?&id=${id}`;
$.getJSON(url)
  .done(function(data) {
    const pet = data.petfinder.pet;
    const pics = pet.media.photos.photo.map(url => url.$t.substr(0, url.$t.indexOf('?'))).filter((val, index, self) => { return self.indexOf(val) === index; });
    const available = pet.status.$t === 'A';
    const title = available ? `Meet ${pet.name.$t}` : `${pet.name.$t} is adopted!`;
    const adoptButton = available ? `
            <div class="clearfix">
              <p class="pull-right"><a class="btn btn-success" href="/adopt/">Adopt ${pet.name.$t}</a></p>
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
          ${pet.description.$t}
          <br />
            <div class="clearfix">
              <p class="pull-right"><a class="btn btn-info" href="https://www.petfinder.com/petdetail/${pet.id.$t}" target="_blank">See ${pet.name.$t} on Petfinder</a></p>
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

