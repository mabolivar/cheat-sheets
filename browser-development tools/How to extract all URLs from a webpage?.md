Here is a quick JavaScript snippet to extract all URLs from a webpage fast with Google Chrome Developer Tools. No Browser Extension is required!

**The JavaScript code generates a list of URLs in CSV format with the anchor texts, and a boolean to know if the URL is internal or external to the current website. Just copy-paste the results into Google Sheets or with the Datablist [CSV editor](https://www.datablist.com/csv-editor).**

> **Notes**: The code works also with Firefox, Safari, etc.


```
const results = [
    ['Url', 'Anchor Text', 'External']
];
var urls = document.getElementsByTagName('a');
for (urlIndex in urls) {
    const url = urls[urlIndex]
    const externalLink = url.host !== window.location.host
    if(url.href && url.href.indexOf('://')!==-1) results.push([url.href, url.text, externalLink]) // url.rel
}
const csvContent = results.map((line)=>{
    return line.map((cell)=>{
        if(typeof(cell)==='boolean') return cell ? 'TRUE': 'FALSE'
        if(!cell) return ''
        let value = cell.replace(/[\f\n\v]*\n\s*/g, "\n").replace(/[\t\f ]+/g, ' ');
        value = value.replace(/\t/g, ' ').trim();
        return `"${value}"`
    }).join('\t')
}).join("\n");
console.log(csvContent)
```

Source: https://www.datablist.com/learn/scraping/extract-urls-from-webpage

