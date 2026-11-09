# Updates for the weekly "Campus events" scheduled task

These recommendations come from the run on 2026-11-06 (target week of 2026-11-09). Apply them to the stored prompt of the scheduled task.

## 1. Source URLs

| Source | Problem in the last run | Replace with |
|---|---|---|
| Econ `https://econ.wisc.edu/workshop-calendar/` | Rendered as an empty heading with no events. `https://econ.wisc.edu/events/` says "No upcoming events." | Use the individual workshop pages as the **primary** Econ source (each lists the semester schedule with speakers and dates):<br>- https://econ.wisc.edu/labor-workshop/ (Mon 3:45, Morton Room 7142 Soc Sci)<br>- https://econ.wisc.edu/public-workshop/ (Tue 3:45, Morton Room)<br>- https://econ.wisc.edu/industrial-organization-workshop/ (Wed 3:45, Morton Room)<br>- https://econ.wisc.edu/macroeconomics-seminar/ (Thu 4:00, Morton Room)<br>- https://econ.wisc.edu/econometrics-seminar/ (Fri 1:30, Morton Room)<br>- https://econ.wisc.edu/theory-seminar/ (Wed 12:20 student talks; Fri 3:45 Morton Room)<br>- https://econ.wisc.edu/international-workshop/ (irregular; check for one-day mini-conferences) |
| Statistics `https://stat.wisc.edu/news-and-events/` | Worked. Event links point to `events.wisc.edu/events/view/<id>`. | Keep it. |
| Philosophy `https://philosophy.wisc.edu/events/colloquia-and-conferences/` | HTTP 404. | Use https://philosophy.wisc.edu/events/ (works; lists colloquia). |
| All three iCal fallbacks (`/events/list/?ical=1`) | HTTP 404 (an HTML error page, not an iCal feed) on econ, stat and philosophy. | Remove them. If a page fails, try the alternates above instead. |

## 2. Tool fallback

WebFetch disappeared from the session's tool list partway through. Add this line: "If WebFetch is unavailable, use the web-fetch subagent or `curl` via Bash. Do not stop the run."

## 3. Speaker flag (UW–Madison Econ, Fall 2005 – Summer 2012)

Replace "check the department's guest-speaker archive or the presenter's CV" with something like this:

> Check each economist presenter against the overlap list below, which comes from the department's PhD placement records. If the name isn't there, check the presenter's CV for a UW–Madison PhD, postdoc, or faculty appointment between 2005 and 2012. Do this check yourself; never leave it for the user. Treat current UW–Madison faculty and students as "UW-affiliated (current)", not as flags.

No guest-speaker archive exists on econ.wisc.edu, but the placement records exist:

- Index: https://econ.wisc.edu/doctoral/career-placement/ (links 2010–11 onward only)
- Older PDFs that aren't linked but still exist at the same URL pattern:
  - https://econ.wisc.edu/wp-content/uploads/sites/725/2017/02/2006-_2007_placement_results.pdf
  - https://econ.wisc.edu/wp-content/uploads/sites/725/2017/02/2007-_2008_placement_results.pdf
  - https://econ.wisc.edu/wp-content/uploads/sites/725/2017/02/2008-_2009_placement_results.pdf
  - https://econ.wisc.edu/wp-content/uploads/sites/725/2017/02/2009-_2010_placement_results.pdf
- Not found (404 on the guessed patterns): 2004–05 and 2005–06.
- Extract the PDFs with `pdftotext -layout`. WebFetch returns raw PDF bytes.

The records only cover PhD graduates. They miss faculty, postdocs, visitors, and students who left without a PhD, so a CV check is still needed for anyone not on the list.

### Overlap list: UW Econ PhDs who were at Madison between Fall 2005 and Summer 2012

**Graduated 2006–07 through 2012–13 (overlap certain):**

- **2006–07:** Bo Chen, Yangsoo Jin, Joong Shik Kang, Jiyoung Kim, Jungwook Kim, Juyoung Kim, Matthew Kim, Mina Kim, Young-Joo Kim, Ratul Lahkar, Michael Malcolm, Enrique Martinez-Garcia, Giacomo Rondina, Jeremy Sandford, Alan Spearot, Jason Wu
- **2007–08:** Ivan Canay, Richard Dunn, John Hore, Shin Kanaya, Chen-Yu Li, Deokwoo Nam, Shiv Saini, Hugette Sun, Nathan Tefft
- **2008–09:** Yasushi Asako, Chikako Baba, Federico Diez, Malcolm Gold, Terrence Iverson, Hojun Lee, Fernando Louge, Nicholas Mader, Hiroaki Miyamoto, Luciana Moscoso Boedo, Francesca Rondina, Dajing Shang, Ping Yu, Wei Zhang
- **2009–10:** Aristoklis Avgousti, Nonarit Bisonyabut, Emmanuele Bobbio, Woo-Hyun Chang, Ben Cowan, Swati Dhingra, Roberto Duncan, Danqing Hu, Ching-Yang (Jim) Lin, Shannon Mok, Ignacio Monzon, David Rivers, Kamil Sicinski, Seung Gyu (Andrew) Sim, Naoya Sueishi, Yuya Takahashi, Alex Yuskavage
- **2010–11:** Katsuhiko Aiba, Mayu Fujii, Kyu-Chul Jung, Sang Yoon (Tim) Lee, Rebecca Lessem, Hiren Nisar, Michael Rapp, Carl Sanders, Jeffrey Traczynski, Xiao Wang, Mian Zhu, Dai Zusai
- **2011–12 (same cohort year as the user):** Camila Casas, Laura Dague, Xiaodong Fan, Chao He, Shengjie Hong, Hon Ho Kwok, Seojeong (Jay) Lee, Haixi Li, Rui Li, Chu-An Liu, Peter Newberry, Enrique Pinzon Garcia, Ryoji Sawa, Mai Seki, Carly Urban, Xiangrong Yu, Ker Zhang
- **2012–13:** Michael Anderson, Laurel Beck, Nicola Branzoli, Atif Chaudry, Yu Fai (Michael) Choi, Francis Flanagan, Seok Ki Kim, Ying-Ying Lee, YoungWook Lee, Hsueh-Hsiang (Cher) Li, Jen-Che Liao, Yusuke Matsuki, Toshinori Onuma, JungJae Park, Saad Quayyum, Nelson Ramirez Rondan, Jiao Shi, Atsuko Tanaka, Hisatoshi Tanaka, Jin Yan, Yuan Yuan

**Graduated 2013–14 (overlap near-certain; entered about 2007–08):**
Andrew Anderson, Wallice Ao, Paola Bordon, Chang Koo Chi, Francisco Franchetti, Serafin Grundl, Nicole Hair, Pedro Hancevic, Erik Hembre, Heewoo (Hugh) Kang, Lihan Liu, Irina Merkurieva, Charalambos (Harry) Michael, Mariann Ollar, Gaston Palmucci, Suphanit Piyapromdee, Nalini Prasad, Fumihiko Suga, Scott Swisher, Jiabin Wu

**Graduated 2014–15 through 2016–17 (likely overlap if they entered by Fall 2011; confirm the entry year):**

- **2014–15:** Drew M. Anderson, Michael Batty, Chi-Yi (Jinny) Chen, Man Wah Cheung, Thomas Conkling, Matthew Friedman, Amanda Gaulke, Gultekin Gollu, Han Han, Benedic Ippolito, Lindsay Jacobs, Yi Li, Hsuan-Chih (Luke) Lin, Tzu-Chi Lin, Zhentong Lu, Kurt Lunsford, Mitchell Morey, Kayuna Nakajima, Hector Gutierrez, Joanna Syrda, Jing Tao, Victoria Udalova, Haomin Wang, Berk Yavuzoglu
- **2015–16:** Vedant Bhatnagar, Jose Antonio Carrasco, Kathryn Edwards, Christa Gibbs, Andrea Guglielmo, Junjie Guo, Joseph Han, Kui (Angela) Huang, Kevin Hutchinson, Byunghoon (David) Kang, Andrew Kidd, Arturo Lamadrid Contreras, Wilson Law, Sean Lewis-Faupel, Chenyan (Monica) Lu, Ryne Marksteiner, Nathan Marwell, Wisarut Suwanprasert, Jianrong Tian, Jorge Vasquez, Gihwan Yi
- **2016–17:** Mark Colas, Kyle Dempsey, Zachary Flynn, Joel Han, Brandon Hoffman, Taehoon Kim, Kanit Kuevibulvanich, Liyi Liu, Irina Shaorshadze, Wei Song, Kegon Tan, Emily Walden, Phillip Warsaw, Woan Foong Wong, Josephine Xu, Nathan Yoder, Yi Zhang

**Missing:** people who graduated in 2005–06 (overlapped one year; no PDF found), plus faculty and postdocs from 2005–2012.

Checked against Fall 2026 speakers: Hao Dong (SMU) and Jason Allen are not in any placement list above.

## 4. Email content

- If every event found is "TBA" and has no new information since last week, consider skipping the email or sending a much shorter one.
- For a TBA talk, the task already says to summarize the presenter's research. Make sure the run actually looks the presenter up instead of guessing from their field.
- Don't put unverified checks in the email as "please check X". Either do the check or say plainly that it couldn't be done and why.
