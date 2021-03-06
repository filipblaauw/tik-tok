# Tidslinje

Based on [Tik Tok](https://github.com/datanews/tik-tok)

## Usage

* Create a timeline in Google spreadsheet - [template spreadsheet](https://docs.google.com/spreadsheets/d/1nr6iRqbUKuBzkuVEXv5L7xC7AUACh-Bj9w5su59HO6o/edit#gid=0)
* Publish it to S3 with Driveshaft, and copy the json url
* Paste the following code to media article in CMS:
```
<link rel="stylesheet" href="http://mm.aftenbladet.no/2016/tik-tok/dist/tik-tok.min.css">
<div id="tik-tok" class="tik-tok-tidslinje">
  <div class="temp-loading">Laster tidslinje...</div>
</div>

<script src="http://mm.aftenbladet.no/2016/tik-tok/bower_components/underscore/underscore.js"></script>
<script src="http://mm.aftenbladet.no/2016/tik-tok/bower_components/moment/moment.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.13.0/locale/nb.js"></script>

<script src="http://mm.aftenbladet.no/2016/tik-tok/dist/tik-tok.min.js"></script>

<script>
  var url = 'http://sa-driveshaft.s3.amazonaws.com/test-tidslinje.json';
  $.getJSON(url, function(data) {
    var tikTok = new TikTok({
      el: '#tik-tok',
      title: 'Nyhetsdøgnet',
      kilde: 'Kilde',
      entries: data.tidslinje
    });
  });
</script>
```
You can change the title and source in the script tag at the end of the code.

Spreadsheet should have the following columns:
* date: `YYYY-MM-DD HH:MM:SS`
* dateDisplay: How date should be displayed. Examples: `DD. MMM, YYYY` or `DD. MMM, YYYY, HH:mm`
* title: Heading in each entry
* body: Text in each entry. Can contain html such as links.
* escenic: ID of the image from Escenic, `123456`
* video: ID of the video from CMS, `123456`
* source: Caption text to the image or video
* article: ID to the read more article. When added, a read more link appears in entry.
