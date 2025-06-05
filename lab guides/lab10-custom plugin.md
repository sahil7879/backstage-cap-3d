to create a custom plugin use this command in your root directory of backstage  
we will be creating a plugin which will give us time and zone fetching the time from time api
```
yarn new
// select frontend plugin
// give the plugin any name you want 
```
in the plugin folder u will see ur new plugin  
if u want to access that plugin go to ip:3000/plugin-name and you will be able to access your plugin that is created by default  
now lets do some changes   
add a new file in components timecard.tsx
```
import { useEffect, useState } from 'react';
import { InfoCard } from '@backstage/core-components';
import { CircularProgress, Typography } from '@material-ui/core';

const TimeCard = () => {
  const [timeData, setTimeData] = useState<any>(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<string | null>(null);

  const timezone = 'Asia/Kolkata'; // You can make this dynamic later

  useEffect(() => {
    const fetchTime = async () => {
      try {
        const response = await fetch(`https://timeapi.io/api/Time/current/zone?timeZone=${timezone}`);
        if (!response.ok) {
          throw new Error('Failed to fetch time');
        }
        const data = await response.json();
        setTimeData(data);
      } catch (err: any) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    };

    fetchTime();
  }, [timezone]);

  return (
    <InfoCard title={`Current Time (${timezone})`}>
      {loading && <CircularProgress />}
      {error && <Typography color="error">Error: {error}</Typography>}
      {timeData && (
        <Typography variant="h6">
          {timeData.date} {timeData.time} ({timeData.dayOfWeek})
        </Typography>
      )}
    </InfoCard>
  );
};

export default TimeCard;
```
index.ts
```
export { default as TimeCard } from './components/timecard';
```
plugin.ts
```
import {
  createPlugin,
  createRoutableExtension,
} from '@backstage/core-plugin-api';
import { rootRouteRef } from './routes';

export const timecardPlugin = createPlugin({
  id: 'timecard',
  routes: {
    root: rootRouteRef,
  },
});

export const TimecardPage = timecardPlugin.provide(
  createRoutableExtension({
    name: 'Timecard',
    component: () =>
      import('./components/timecard').then(m => m.default),
    mountPoint: rootRouteRef,
  }),
);
```
now lets add this in frontend app  
in app.txs
change the import and route from timepage to timecard
and in entitypage.tsx add this block where you want to display time 
```
<Grid item md={3}>
      <TimeCard /> {/* Your custom card */}
    </Grid>

```
