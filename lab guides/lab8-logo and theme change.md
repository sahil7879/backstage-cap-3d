make some changes in this file \backstage\packages\app\src\components\Root\Logofull.tsx
```
const useStyles = makeStyles({
  svg: {
    width: 'auto',
    height: 40,
  },
  path: {
    fill: '#7df3e1', // Adjust color to match your logo
  },
});
const LogoFull = () => {
  const classes = useStyles();
  // Replace this with your logo (as SVG or <img>)
  return (
    <img 
      src="/download.png" 
      alt="Company Logo" 
      className={classes.svg}
    />
  );
};
export default LogoFull;
```
make change in this file to edit your logo packages\app\src\components\Root\LogoIcon.tsx
```
import { makeStyles } from '@material-ui/core/styles';
const useStyles = makeStyles({
  svg: {
    width: 24,
    height: 24,
  },
});
const LogoIcon = () => {
  const classes = useStyles();
  return (
    <img 
      src="/download.png" 
      alt="Company Icon" 
      className={classes.svg}
    />
  );
};
export default LogoIcon;

```
for theme change add a new dir in components  
```
backstage\packages\app\src\themes\customtheme.ts

import {
  createBaseThemeOptions,
  createUnifiedTheme,
  palettes,
 
} from '@backstage/theme';
export const myTheme = createUnifiedTheme({
  ...createBaseThemeOptions({
    palette: {
      ...palettes.dark,
      primary: {
        main: '#111',
      },
      secondary: {
        main: '#111',
      },
      background: {
        default: '#2f4c9c',
        paper: '#432f9c',
      },
    }})
});
```
to add this theme 
do these imports in App.tsx
```
import LightIcon from '@material-ui/icons/WbSunny';
import { UnifiedThemeProvider} from '@backstage/theme';
import { myTheme } from './themes/customtheme';
```
