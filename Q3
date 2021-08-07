const puppeteer = require('puppeteer');
var FilterArray = [];
const args = process.argv;
(async () => {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  await page.goto('https://codequiz.azurewebsites.net/');
  await page.waitForSelector('body > input[type=button]');
  await page.click('body > input[type=button]')
  await page.screenshot({
    path: "./screenshot.png",
    fullPage: true
  });
  const ROW = await page.evaluate(() => {
    const rows = document.querySelectorAll('table tr');
    return Array.from(rows, row => {
      const columns = row.querySelectorAll('td');
      return Array.from(columns, column => column.innerText);
    });
  });
  ROW.forEach(r => {
    if(r[0]){
      FilterArray.push([r[0],r[1]])
    }
  });
  FilterArray.forEach(f => {
    if(args[2] == f[0]){
      console.log(f[1])
    }
  });
  await browser.close();
})();
