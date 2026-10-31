| Cell | Metric | Formula |
| --- | --- | --- |
| B3 | Total leads | `=COUNTA(Leads!C2:C)` |
| B4 | New leads, last 7 days | `=COUNTIFS(Leads!A2:A,">="&(TODAY()-7))` |
| B5 | Average score | `=IFERROR(ROUND(AVERAGE(Leads!L2:L),1),0)` |
| B6 | Stage: Lead | `=COUNTIF(Leads!M2:M,"Lead")` |
| B7 | Stage: MQL | `=COUNTIF(Leads!M2:M,"MQL")` |
| B8 | Stage: SQL | `=COUNTIF(Leads!M2:M,"SQL")` |
| B9 | SQL share | `=IFERROR(B8/B3,0)` |
| B10 | Free-email leads | `=COUNTIF(Leads!I2:I,"Free email")` |
| B11 | Interested in automation | `=COUNTIF(Leads!G2:G,"Automation")` |
| B13 | Email summary | `="<h2>Weekly lead report</h2><p><b>"&B4&"</b> new leads in the last 7 days ("&B3&" in total).</p><p>Pipeline: "&B6&" Lead, "&B7&" MQL, "&B8&" SQL ("&TEXT(B9,"0%")&" SQL). Average score: "&B5&".</p><p>"&B10&" leads used a free email address; "&B11&" are interested in automation.</p>"` |
