$.fn.computeLink = function (link, index) {
  return link !== undefined && link !== false ? link : "#permalink" + index;
};

$.fn.loadNews = function (nbNewsToDisplay) {
  $.ajax({
    type: "GET",
    url: "news/news.xml",
    dataType: "xml",
    success: function (xml) {
      let itemIndex = $(xml).find("item").length;

      $(xml)
        .find("item")
        .filter(function (index) {
          return index < nbNewsToDisplay;
        })
        .each(function () {
          $("#news-news").append(
            "<b>" +
              '<a name ="permalink' +
              itemIndex +
              '"></a>' +
              "<a href=" +
              $(this).computeLink($(this).attr("link"), itemIndex) +
              ' target="_blank">' +
              $(this).attr("title") +
              "</a><br>" +
              "Posted " +
              new Date($(this).attr("date")).toLocaleDateString("en-us", {
                year: "numeric",
                month: "short",
                day: "numeric",
              }) +
              "</b>" +
              '<p class="text-justify"></p>' +
              '<p class="text-justify">' +
              $(this).html() +
              "</p>" +
              "<p></p>" +
              '<hr class="custom-divider">'
          );
          itemIndex = itemIndex - 1;
        });
    },
  });
};

$.fn.loadQuotes = function () {
  $.ajax({
    type: "GET",
    url: "quotes/quotes.xml",
    dataType: "xml",
    success: function (xml) {
      let itemIndex = $(xml).find("quote").length;
      $("#quotes-quotes").append("<div>");
      $(xml)
        .find("quote")
        .eq(Math.floor(Math.random() * itemIndex))
        .each(function () {
          $("#quotes-quotes").append(
            "<div>" +
              '<p class="text-justify"><img class="openquote" src="img/openquote.png" alt="Open quote"/>' +
              $(this).html() +
              '<img class"closequote" src="img/closequote.png" alt="Close quote"/></p>' +
              '<p class="text-right"><b><em>' +
              $(this).attr("author") +
              "</em></b></p>" +
              "</div>"
          );
        });

      $("#quotes-quotes").append("</div>");
    },
  });
};

$.fn.shuffle = function () {
  let xmlContent = this;
  for (let i = 0; i < xmlContent.length - 1; i++) {
    let j = i + Math.floor(Math.random() * (xmlContent.length - i));

    let temp = xmlContent[j];
    xmlContent[j] = xmlContent[i];
    xmlContent[i] = temp;
  }
  return xmlContent;
};

$.fn.loadApplications = function () {
  $.ajax({
    type: "GET",
    url: "applications/applications.xml",
    dataType: "xml",
    success: function (xml) {
      let itemIndex = $(xml).find("application").length;
      $("#applications-applications").append("<div>");
      $(xml)
        .find("application")
        .shuffle()
        .filter(function (index) {
          return index < 3;
        })
        .each(function () {
          $("#applications-applications").append(
            '<div class="col-sm-4"> ' +
              '<a href="' +
              $(this).attr("resource") +
              '" target="_blank">' +
              '<img class="img-responsive center-block application-img" src="' +
              $(this).attr("logo") +
              '" alt="' +
              $(this).attr("author") +
              '" + "Use Case Story">' +
              "</a>" +
              '<b>"' +
              $(this).html() +
              '"</b><br>' +
              $(this).attr("author") +
              "</div>"
          );
        });

      $("#applications-applications").append("</div>");
    },
  });
};
/*
$(document).ready(function () {
  $.fn.loadNews(5);
  $.fn.loadQuotes();
  $.fn.loadApplications();
}); */
/*
$.fn.generateRSS = function () {
  $.ajax({
    type: "GET",
    url: "news/news.xml",
    dataType: "xml",
    success: function (xml) {
      let xmlDoc = document.implementation.createDocument('', '', null);
      let root = xmlDoc.createElement('root');
        
      $(xml)
        .find("item")
        .each(function () {
          // console.log($(this).html());
          let child = xmlDoc.createElement('child');
          child.textContent = $(this).html();
          root.appendChild(child);
        });

        xmlDoc.appendChild(root);
        let xmlString = new XMLSerializer().serializeToString(xmlDoc);
        let blob = new Blob([xmlString], { type: 'application/xml' });
        let url = URL.createObjectURL(blob);
        window.open(url, '_self');

        setTimeout(() => {
          URL.revokeObjectURL(url);
      }, 1000);
    },
  });
  return('<?xml version="1.0" encoding="UTF-8"?><rss>feed</rss>');
}; */
/*
$.fn.generateRssButton = function () {
  console.log("xxxxxxxxxxxxxxxxxx")
  // Créer le document RSS
  let rssDoc = document.implementation.createDocument('', '', null);
  
  // Créer l'élément racine <rss>
  let rss = rssDoc.createElement('rss');
  rss.setAttribute('version', '2.0');
  
  // Créer l'élément <channel>
  let channel = rssDoc.createElement('channel');
  
  // Ajouter des éléments au <channel>
  let title = rssDoc.createElement('title');
  title.textContent = 'Mon Flux RSS';
  channel.appendChild(title);
  
  let link = rssDoc.createElement('link');
  link.textContent = 'http://www.example.com';
  channel.appendChild(link);
  
  let description = rssDoc.createElement('description');
  description.textContent = 'Ceci est un flux RSS exemple.';
  channel.appendChild(description);
  
  // Ajouter un élément <item>
  let item = rssDoc.createElement('item');
  
  let itemTitle = rssDoc.createElement('title');
  itemTitle.textContent = 'Titre de l\'article';
  item.appendChild(itemTitle);
  
  let itemLink = rssDoc.createElement('link');
  itemLink.textContent = 'http://www.example.com/article';
  item.appendChild(itemLink);
  
  let itemDescription = rssDoc.createElement('description');
  itemDescription.textContent = 'Ceci est la description de l\'article.';
  item.appendChild(itemDescription);
  
  channel.appendChild(item);
  rss.appendChild(channel);
  rssDoc.appendChild(rss);
  
  // Convertir le document RSS en chaîne de caractères
  let rssString = new XMLSerializer().serializeToString(rssDoc);
  
  // Créer un Blob à partir de la chaîne RSS
  let blob = new Blob([rssString], { type: 'application/rss+xml' });
  
  // Créer une URL Blob
  let url = URL.createObjectURL(blob);
  
  // Ouvrir le document RSS dans une nouvelle page vierge dans le même onglet
  // window.location.href = url;
  window.open(url, '_self');
  
  // Révoquer l'URL de l'objet pour libérer de la mémoire (optionnel)
  setTimeout(() => {
      URL.revokeObjectURL(url);
  }, 1000);
}; */
