---
layout: default
title: About
permalink: /about/

people:
 - 
    name: Daniel
    pic: http://k94keeps.org/images/board_daniel.png
    desc: Daniel is the President and a founding member of K9 4 KEEPS. Daniel has been rescuing dogs in need and placing them in quality homes for many years before helping found K9 4 KEEPS. When Daniel isn’t doing rescue work, he is training clients’ dogs in obedience, taking his girl dog Jelly to do animal-assisted therapy work, and training working dogs in protection sport for Windy City Working Dogs, Inc. Daniel’s favorite part of rescue is helping people and dogs have a positive impact on each other’s lives. 
 -
    name: Caroline
    pic: http://k94keeps.org/images/board_caroline.png
    desc: Caroline is the Vice President of K9 4 KEEPS. Caroline started as a volunteer dog walker a few months after K9 4 KEEPS’ launch and has handled many of our dogs as they have gone through training. She became a board member in March of 2013. When Caroline isn’t doing rescue, she is involved in animal-assisted therapy with Louie and protection sport training with Kaiser. Her pit bull, Gypsy (adopted from K9 4 KEEPS) is also deaf, so she has a soft spot for bully breeds and special-needs rescues. Caroline’s favorite part of rescue is walking a dog out of an open-access shelter to freedom. 
 -
    name: Amy
    pic: http://k94keeps.org/images/board_amy.png
    desc: Amy is the Treasurer and a founding member of K9 4 KEEPS. Along with Daniel, Amy has many years of experience rescuing and re-homing dogs. She is our resident “mama dog and puppies” guru, graphic design expert, and the glue that holds K9 4 KEEPS together. When Amy isn’t doing rescue, she is doing animal-assisted therapy work with Jelly Belly Butterfly, snuggling Peace, and running Bark Avenue Playcare. Amy’s favorite part of rescue is seeing a homeless dog become a beloved family member. 
 -
    name: Kelly
    pic: http://k94keeps.org/images/board_kelly.png
    desc: Kelly is the Secretary of K9 4 KEEPS. Kelly started as a wonderful foster mom and volunteers so much of her time to plan fundraising events for our rescue and take beautiful photographs of our adoptable dogs. Kelly became a board member in July of 2014. When Kelly isn’t doing rescue, she is involved in protection sport training with Knox, photography, and social outings around the city. Kelly’s favorite part of rescue is finding great forever homes for all of our awesome dogs. 
 -
    name: Erin
    pic: http://k94keeps.org/images/board_erin.png
    desc: Erin is the Event Coordinator of K9 4 KEEPS. Erin started volunteering as a dog handler at adoption events and works tirelessly to market, plan, and execute fundraising and social events. Erin became a board member in September of 2014. When Erin isn’t doing rescue, she is involved in protection sport training with Mishy, running, and taking Mishy and Rocky for marathon walks followed by marathon couch snuggle sessions. Erin’s favorite part of rescue is being the voice for those who don’t have one. 
---
<div class="container">

<h1>About</h1>

K9 4 KEEPS, NFP believes that bringing a dog into your family should be forever. For keeps. We are a 100% volunteer run, 501(c)(3) non-profit organization dedicated to dog rescue. We believe rescue should begin with education and counseling of dog owners regarding proper handling and training of their dogs to support positive, forever relationships. K9 4 KEEPS dogs are surrendered by their owners or rescued from Chicagoland area kill shelters and are provided vetting, housing, foster and adoption services.

<h2>History</h2>

The seeds of K9 4 KEEPS, NFP were planted way back in 2000 when Amy and Daniel adopted their first dog, Otto. He was a 10 month old, 90 lb. Rottweiler. Otto was adopted from a local rescue and was followed by a couple of foster dogs including Maximus, another Rottie and their first “foster‐failure.” Amy and Daniel became inspired by Otto and Max to start [Bark Avenue Playcare, Inc](http://www.barkavenueplaycare.com/) and also get more involved with dog (and the occasional cat) rescue. 

Like most people in the rescue world, they helped a few different organizations and met a lot of truly dedicated people. Bark Avenue became a rescue resource early on with the first employees being hired to care for some of these organization’s rescue dogs which were in boarding. Amy and Daniel started to see the actual scope of the homeless/abused/neglected animal situation in Chicago. Through their involvement with friends and contacts in the “dog world”, they realized that more could be done if they could create a network of people who shared their goals of responsible rescue and ownership. 

K9 4 KEEPS, NFP was born from the hope that we could make an impact on the homeless/abused/neglected dog problems in the Chicago area and empower more people to make a difference. K9 4 KEEPS, NFP was founded by Amy and Daniel with the help of the rest of our original Board members. The current Board has continued the original mission to impact the homeless/abused/neglected dog population of the Chicago area and empower people to make a difference. 

<h2>Board Members</h2>

{% for person in page.people %}
  {% assign mod = forloop.index | modulo: 2 %}
  <div class="row">
    <div class="col-md-7 {% if mod == 0 %}col-md-push-5{% endif %}" >
      <h3>{{ person.name }}</h3>
      <p>{{ person.desc }}</p>
    </div>
    <div class="col-md-5 {% if mod == 0 %}col-md-pull-7{% endif %}">
      <img class="img-responsive center-block" src="{{ person.pic }}" alt="{{ person.name }}" style="max-height: 300px;">
    </div>
  </div>
{% endfor %}
</div><!-- /.container -->
