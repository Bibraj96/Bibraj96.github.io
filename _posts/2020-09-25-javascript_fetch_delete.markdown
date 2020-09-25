---
layout: post
title:      "JavaScript: Fetch DELETE"
date:       2020-09-25 15:14:56 +0000
permalink:  javascript_fetch_delete
---


For my JavaScript portfolio project I made a single-page application(SPA) that lets users post animal sightings at a zoo of his/her/their choice. As far as database relationships go, a Zoo has many Sightings and a Sighting belongs to a Zoo. If a desired zoo isn't found, one can be added so that everyone else can add sightings to it as well. Bootstrap was used to style the SPA.

When I first started implementing the fetch requests, things went quite smoothly. This was because I was simply retrieving all of the zoos using the `http://localhost:3000/zoos` URL from my Rails API, so I didn't need to dynamically add an `id` to the URL. However when it came time to delete a zoo, I realized that my DOM needed better structuring so that I could manipulate it properly.

The most important thing I needed to do was to add a `data` attribute for the `id` of the zoo, so that I could retrieve it by traversing the DOM. I ended up adding a `data-zoo-${zoo.id}` attribute to the zoos `div` that dynamically added the zoo's `id`. This allowed me to easily grab it whenever I needed it.

```
function deleteZoo() {
  let zooId = this.parentElement.getAttribute('data-zoo-id')

  fetch(`http://localhost:3000/zoos/${zooId}`, {
    method: 'DELETE',
    headers: {'Content-Type': 'application/json', 'Accept': 'application/json'}
  })
  .then(resp => resp.json())
  .then(json => {
    let selectedZoo = document.querySelector(`.container[data-zoo-id="${zooId}"]`)
    selectedZoo.remove()
  })
}
```

In the second line of the code block above, `let zooId = this.parentElement.getAttribute('data-zoo-id')`, I traverse the DOM to grab the appropriate zoo id from the `data` attribute and dynamically place it in the URL I'm using for my fetch call, `fetch('http://localhost:3000/zoos/${zooId}'`. This allows me to grab the specific show path from my Rails API and delete the correct record.

This was one of many roadblocks I ran into while working on this project, which proved to be the most difficult one for me in the bootcamp so far. I'm excited to submit it and learn more in my project review!
