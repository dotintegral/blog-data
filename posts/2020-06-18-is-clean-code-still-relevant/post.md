---
date: 2020-06-18
published: true
title: Is the Clean Code still relevant in frontend development?
tags:
  - clean code
  - patterns
  - book review
description:
  Over a decade ago, Robert C. Martin published an excellent book called "Clean Code".
  But is it still relevant in modern frontend environment?
cover_image: cover.jpg
---

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque diam eros, pharetra eget dui vel, tristique efficitur mi. Sed ut fermentum diam, sed dapibus lectus. Nam vitae orci sed lectus tristique rhoncus sit amet vel quam. Proin tristique nulla ut sem scelerisque, a mattis libero dignissim. Praesent imperdiet dolor lorem, ac rutrum elit rutrum et. Cras et nulla et urna convallis volutpat. Sed auctor imperdiet bibendum. Quisque ultricies pulvinar sem, eget dictum quam lacinia vel. Praesent ut nisl id risus tincidunt tristique. Sed vel mi non nulla pulvinar consequat a a turpis. Aliquam metus ex, pharetra vitae convallis vel, cursus quis nibh. Donec venenatis congue lorem, ut tempor urna tincidunt eget. Sed feugiat justo varius leo venenatis, in consectetur lectus mattis. In ullamcorper nulla nec luctus vulputate. Suspendisse quis arcu finibus, imperdiet ante mattis, porttitor neque.

Maecenas in semper lacus. Etiam at lacus odio. Mauris lacus erat, ultrices vitae erat vitae, vehicula interdum metus. Suspendisse dolor odio, accumsan in viverra at, bibendum lobortis felis. Fusce euismod sagittis tristique. Aenean vestibulum, ex ac fringilla fringilla, erat dui venenatis risus, sed vulputate neque neque vel dolor. Vivamus elementum rhoncus est eget aliquam. Phasellus fringilla ultrices nisl, id venenatis nisl malesuada vitae. Quisque quis magna leo. Aliquam vestibulum arcu at diam ullamcorper cursus sagittis quis nisl. Pellentesque et turpis dolor. Quisque pellentesque turpis sit amet lacus porttitor pulvinar. Nulla at nunc ut neque dictum ullamcorper.

```javascript
function compareValues(key, order = "asc") {
  return function innerSort(a, b) {
    if (!a.hasOwnProperty(key) || !b.hasOwnProperty(key)) {
      // property doesn't exist on either object
      return 0;
    }

    const varA = typeof a[key] === "string" ? a[key].toUpperCase() : a[key];
    const varB = typeof b[key] === "string" ? b[key].toUpperCase() : b[key];

    let comparison = 0;
    if (varA > varB) {
      comparison = 1;
    } else if (varA < varB) {
      comparison = -1;
    }
    return order === "desc" ? comparison * -1 : comparison;
  };
}
```

Nam molestie magna at varius commodo. Etiam lobortis varius lorem, rutrum rhoncus augue fermentum id. Proin vestibulum eu lacus sit amet volutpat. Vivamus mi dui, faucibus at libero id, pulvinar tincidunt nulla. Cras iaculis turpis id tincidunt consequat. Phasellus sagittis, velit id dapibus mattis, urna ex dignissim enim, id pharetra tellus sem non dolor. Integer tempor mollis tortor, eu venenatis sem posuere euismod. Donec finibus hendrerit est, eget porta ipsum viverra eget. Aliquam erat volutpat. Mauris a finibus elit. Cras ut eros ante. Etiam id eros semper, faucibus magna at, ultrices dolor. Interdum et malesuada fames ac ante ipsum primis in faucibus. Sed eu dignissim quam, vitae rutrum mi. Quisque ullamcorper quis nulla ut pretium.

Phasellus in lorem massa. Etiam erat urna, porta quis pellentesque quis, hendrerit ullamcorper nisi. Sed vitae placerat neque. Phasellus vitae suscipit nisi, quis vulputate tellus. Sed arcu metus, dapibus sed mi ut, luctus convallis mi. Quisque at fermentum ante. Nullam nec finibus velit. Proin fermentum tellus quis eros lacinia faucibus. Cras at lectus ex. In ullamcorper ante eget quam dignissim cursus vitae nec est. Suspendisse at commodo neque.

```javascript
function compareValues(key, order = "asc") {
  return function innerSort(a, b) {
    if (!a.hasOwnProperty(key) || !b.hasOwnProperty(key)) {
      // property doesn't exist on either object
      return 0;
    }

    const varA = typeof a[key] === "string" ? a[key].toUpperCase() : a[key];
    const varB = typeof b[key] === "string" ? b[key].toUpperCase() : b[key];

    let comparison = 0;
    if (varA > varB) {
      comparison = 1;
    } else if (varA < varB) {
      comparison = -1;
    }
    return order === "desc" ? comparison * -1 : comparison;
  };
}
```

Aenean non nulla imperdiet, semper enim id, rhoncus quam. Sed nec lacus fringilla, dictum metus porta, vehicula enim. Sed est ex, feugiat ac tincidunt sed, fermentum tincidunt metus. Ut id odio lobortis, viverra nulla vel, euismod sapien. Nullam aliquam massa eu magna laoreet, sed egestas sem tempor. Vestibulum blandit cursus semper. In hac habitasse platea dictumst. Aenean nec consequat urna. Curabitur auctor mi mi, ut rhoncus est elementum at. Integer viverra ipsum eget accumsan sodales. Praesent facilisis tincidunt enim. Nullam scelerisque id purus a posuere.
