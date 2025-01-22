### Copy pasted this from here 
https://gist.github.com/iamandrewluca/9e46589f42545446fa387ac193c43634
```
(function bookmarksExportToCsv() {
  /**
   * 1. Export bookmarks from browser (supported any Chromium based browsers and Safari) (chrome://bookmarks)
   * 2. Open exported html file again in the browser
   * 3. Copy paste this entire file in console, and execute it (hit enter)
   * 4. You will be prompted to save a CSV file. Save it.
   * 5. Open Notion. Click Import -> CSV
   * 6. Select saved CSV file. Wait for import
   * 7. You have a new database with all your bookmarks
   */
  const bookmarks = getBookmarks(document.body);
  const csvString = arrayToCsv(bookmarks);
  downloadString(csvString);

  function getBookmarks(def, tags = []) {
    // Chromium browsers exports dl first
    // Safari browser exports dt first
    // We take both into consideration
    return Array.from(def.querySelectorAll(":scope > dl, :scope > dt")).flatMap(
      function (child) {
        // Find for a bookmark
        const anchor = child.querySelector(":scope > a");
        return anchor
          ? // if found create a bookmark object from it
            createBookmark(anchor, tags)
          : // if not, we go down in the tree, adding a new tag in tags
            getBookmarks(child, getNewTags(tags, child));
      }
    );
  }

  function createBookmark(anchor, tags) {
    return {
      Name: anchor.innerText,
      Created: getDate(anchor),
      Tags: tags.join(", "),
      // Make sure URL's are encoded, otherwise, Notion may fail to import
      Url: encodeURI(anchor.href),
    };
  }

  function getDate(anchor) {
    const stringDate = anchor.getAttribute("add_date");
    // Safari does not add an add_date attribute, default to new Date
    const date = stringDate ? new Date(Number(stringDate) * 1000) : new Date();
    const dateF = new Intl.DateTimeFormat("en-US", { dateStyle: "medium" });
    const hourF = new Intl.DateTimeFormat("en-US", { timeStyle: "short" });
    // Notion it seems to support it this way
    return `${dateF.format(date)} ${hourF.format(date)}`;
  }

  function getNewTags(tags, def) {
    // Depending on depth level heading can be different
    const heading = def.querySelector(
      [
        ":scope > h1",
        ":scope > h2",
        ":scope > h3",
        ":scope > h4",
        ":scope > h5",
        ":scope > h6",
      ].join(",")
    );
    if (!heading) return tags;
    return [...new Set([...tags, heading.innerText])]
  }

  function arrayToCsv(array) {
    const titles = ["Name", "Created", "Tags", "Url"].map((t) => `"${t}"`);

    const entries = array.map((e) =>
      [e.Name, e.Created, e.Tags, e.Url]
        // We use double quotes as data wrapper
        // We escape double quotes inside using another double quote as RFC says
        .map((f) => `"${f.replace(/"/g, `""`)}"`)
        .join(",")
    );

    return `${titles.join(",")}\n${entries.join("\n")}`;
  }

  function downloadString(text) {
    const a = document.createElement("a");
    a.href = window.URL.createObjectURL(new Blob([text], { type: "text/csv" }));
    // When importing in Notion it will use file name without extension as page name
    a.download = "Bookmarks.csv";
    a.click();
    window.setTimeout(() => window.URL.revokeObjectURL(a.href));
  }
})();
```
