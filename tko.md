
*While this site does not represent [Trek Bicycle Corporation](https://www.trekbikes.com) or their [O'Fallon, MO shop](https://www.trekbikes.com/us/en_US/retail/o_fallon/), I have found a great community of friendly, welcoming folks there and thought I'd share some useful information for those who may be interested in joining the community.*

First things, first: Everyone is welcome to join the group rides! Are you new? [Check out the new rider guide](newrider.md) for some tips and encouragement!

<div id="sat-hours-weather"
     style="padding:12px;background:#eef6ff;border-radius:8px;
            font-family:Arial, sans-serif;width:340px;">
  Loading next Saturday's 8AM–Noon forecast...
</div>

<script>
async function loadSaturdayHours() {
  const lat = 38.8106;   // O'Fallon, MO
  const lon = -90.6998;

  // Step 1: Get forecast URLs for this point
  const pointRes = await fetch(`https://api.weather.gov/points/${lat},${lon}`);
  const pointData = await pointRes.json();
  const hourlyUrl = pointData.properties.forecastHourly;

  // Step 2: Fetch hourly forecast
  const hourlyRes = await fetch(hourlyUrl);
  const hourlyData = await hourlyRes.json();
  const periods = hourlyData.properties.periods;

  // Step 3: Determine next Saturday
  const now = new Date();
  const nextSat = new Date(now);
  nextSat.setDate(now.getDate() + ((6 - now.getDay() + 7) % 7 || 7));
  nextSat.setHours(8, 0, 0, 0);

  // Format date for display
  const dateStr = nextSat.toLocaleDateString([], {
    weekday: 'long',
    month: 'long',
    day: 'numeric'
  });

  // Step 4: Collect hours 8AM → Noon
  const targets = [];
  for (let h = 8; h <= 12; h++) {
    const hourDate = new Date(nextSat);
    hourDate.setHours(h);

    const match = periods.find(p => {
      const d = new Date(p.startTime);
      return d.getHours() === hourDate.getHours() &&
             d.getDate() === hourDate.getDate();
    });

    if (match) targets.push(match);
  }

  const box = document.getElementById("sat-hours-weather");

  if (targets.length === 0) {
    box.innerText = "No Saturday hourly forecast available yet.";
    return;
  }

  // Step 5: Render the table with date
  let html = `<strong>Next Saturday (${dateStr})</strong><br>
              <em>Hourly Forecast: 8AM–Noon</em><br><br>
              <table style="width:100%;font-size:14px;">
                <tr><th align="left">Time</th>
                    <th align="left">Temp</th>
                    <th align="left">Precip</th>
                    <th align="left">Wind</th></tr>`;

  targets.forEach(t => {
    const d = new Date(t.startTime);
    const time = d.toLocaleTimeString([], { hour: 'numeric' });
    const precip = t.probabilityOfPrecipitation.value ?? 0;

    html += `<tr>
               <td>${time}</td>
               <td>${t.temperature}°${t.temperatureUnit}</td>
               <td>${precip}%</td>
               <td>${t.windSpeed} ${t.windDirection}</td>
             </tr>`;
  });

  html += `</table>`;
  box.innerHTML = html;
}

loadSaturdayHours();
</script>


## Getting Connected
The best way to get connected is to go by the shop! Grab a cup of coffee (or an NA beer), hang out and talk bikes! In addition to that, you can connect with the community online...

[<img src="images/Strava.png" style="vertical-align: middle;" />](https://www.strava.com/clubs/1181950/)
[<img src="images/fb.png" style="vertical-align: middle;" />](https://www.facebook.com/TrekBicycleOFallon)
[<img src="images/Discord.png" style="vertical-align: middle;" />](https://discord.gg/dhuePbFFDT)

A great way to stay in touch with cycling happenings is via the [shop's Strava Club](https://www.strava.com/clubs/1181950). You'll see regular updates on group rides as well as other fun reasons to get together and enjoy cycling as a crew.

## Group Rides
One of the things I love most about the Trek O'Fallon Cycling Community is the group rides. Through these, I have met great folks, learned a lot, and had a great time pursuing a great pastime.  

### Saturday Morning Road Rides
The most popular event for the crew is the **Saturday Morning Road Ride** which is a social, no-drop ride. 

**Who:** Cyclists of _all_ abilities are welcome. We break into groups by ability from a casual ~17 MPH pace to our A group that runs 21+ MPH.  
If you're like me, you may worry that you'll be the newest, the slowest, or just not up to the task. This couldn't be further from the truth. This group makes sure even the slowest rider has a great time and learns a lot. The Trek crew drops back to ensure that you're included and there's never any concern that a rider is "holding them back."  

**When:**  Saturday Mornings, 8:00 AM, *weather permitting*  (The ride will generally be moved to a [virtual ride](#virtual-group-rides) if there is precipitation, crosswinds exceeding 30 mph, or windchill below 10 degrees Fahrenheit)

**Where:** We meet at Trek O'Fallon, 8640 Mexico Rd., O'Fallon, MO. From there, the group generally takes one of two routes:
- **[River Flats Route](https://ridewithgps.com/routes/53566458?privacy_code=9UlQabM2C2IoD8j8U4vbIXAscpfgRMBg):** 42.5 miles with only 618 feet of climbing. The group stops frequently to regroup, refuel and hydrate. There are even bathroom stops!
- **[St. Paul Country Rollers Route](https://ridewithgps.com/routes/53566477?privacy_code=84szbLq1vQUGQXxbk9iHX9FRJn5KLofS):**  29.7 miles with 1313 feet of climbing. Again, plenty of stops to regroup and recharge.  

If you have a Garmin, Wahoo, or other GPS device, you can download these routes to help guide you along the way.

### Virtual Group Rides
In the event of inclement weather, many of us join up on the [ROUVY](https://rouvy.com/) virtual cycling platform. We'll start at the normal time, but ride the virtual version of one of our favorite routes:  

| Route | Distance | Climbing |  
|-------|----------|-----------|  
| [St. Paul Route](https://riders.rouvy.com/route/266126) | 23.89 mi | 994 ft |  
| [River Flats Ride](https://riders.rouvy.com/route/275858) | 39.5 mi | 541 ft |  
| [Rainy Fall SMR](https://riders.rouvy.com/route/252194) | 38.24 mi | 804 ft |   

Which route we'll ride is usually announced via the [Strava Club](https://www.strava.com/clubs/1181950) and/or the [Facebook page](https://www.facebook.com/TrekBicycleOFallon).  To keep it fun and social, we join voice chat on the community's [Discord channel](https://discord.gg/dhuePbFFDT).

<iframe src="https://discord.com/widget?id=1442264364743786599&theme=dark" width="350" height="500" allowtransparency="true" frameborder="0" sandbox="allow-popups allow-popups-to-escape-sandbox allow-same-origin allow-scripts"></iframe>

