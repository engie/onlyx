---
layout: default
title: TRMNL School Menu
nav_order: 4
---
I've hacked up a [TRMNL](https://usetrmnl.com/) private plugin to display [Hampshire primary school meals](https://www.hants.gov.uk/educationandlearning/education-catering/parent-information/primary).
![A photo of a TRMNL screen showing the meat, meat free and dessert options for Today(Friday) and Monday in the Hampshire Primary School Catering menu](/assets/images/menu.png){:style="display:block; margin-left:auto; margin-right:auto"}

### Dev notes
[Code on GitHub https://github.com/engie/menu](https://github.com/engie/menu)
* I originally planned to run a cloudflare worker to fetch menu data live, but that was annoying as the menu website has cloudflare scraping protection. Overall it doesn't change very often so a simple download, with local scripts to extract the relevant data, ended up much cleaner. You can load a blob of JSON as static data into the TRMNL system, although this failed before I got round to deduping the images (with a 4MB file), at roughly 85KB it's fine.
* ChatGPT O3 did a good job of writing the [scraping code](https://github.com/engie/menu/blob/main/get_menu/extract.py). It enjoyed first asking ChatGPT to read the site and generate JSON itself, then to write code to do the same, then to compare the outputs & fix any discrepencies. It did a great job for this, and writing scraping code by hand is no fun.
* I used DALL-E-3 to [generate the icons](https://github.com/engie/menu/blob/main/get_menu/generate_menu_icons.py). This went OK, not as good as interactively asking O3 to do so. I may come back to debug this prompt later. Was fun working with O3 on this code, including using the ChatGPT VSCode integration.
* The [HTML template](https://github.com/engie/menu/blob/main/full.liquid) is pretty horrible, fiddly and I was editing it in the TRMNL app. It worked in the end, but overall poor dev experience here.