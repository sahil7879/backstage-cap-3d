add a button file  
create a dir  
packages/app/src/components/button/button.tsx
```
import Button from '@mui/material/Button';
import { styled } from '@mui/material/styles';
const StyledButton = styled(Button)(({}) => ({
  backgroundColor: '#0072ce',
  color: 'white',
  borderRadius: 8,
  padding: '8px 16px',
  fontWeight: 'bold',
  '&:hover': {
    backgroundColor: '#005bb5',
  },
}));
type BrandedButtonProps = {
  label: string;
  onClick: () => void;
};
export const BrandedButton = ({ label, onClick }: BrandedButtonProps) => {
  return <StyledButton onClick={onClick}>{label}</StyledButton>;

};
```

for custom filters create a new dir in components named filter  
add these files in there  
custompicker.tsx
```
import {
  Checkbox,
  FormControl,
  FormControlLabel,
  FormGroup,
  Typography,
} from '@material-ui/core';
import { useEntityList } from '@backstage/plugin-catalog-react';
import { EnvironmentFilter } from './customfilter';
import { CustomFilters } from './customFil';
export const EnvironmentPicker = () => {
  const {
    filters: { environment },
    updateFilters,
  } = useEntityList<CustomFilters>();
  const toggle = (value: string) => {
    const current = environment?.values ?? [];
    const updated = current.includes(value)
      ? current.filter(t => t !== value)
      : [...current, value];
    updateFilters({
      environment: updated.length ? new EnvironmentFilter(updated) : undefined,
    });
  };
  const envOptions = ['dev', 'qa', 'prod'];
  return (
    <FormControl component="fieldset">
      <Typography variant="button">Environment</Typography>
      <FormGroup>
        {envOptions.map(env => (
          <FormControlLabel
            key={env}
            control={
              <Checkbox
                checked={environment?.values.includes(env) ?? false}
                onChange={() => toggle(env)}
              />
            }
            label={env.toUpperCase()}
          />
        ))}
      </FormGroup>
    </FormControl>
  );
};

```
customfilter.tsx
```

import { Entity } from '@backstage/catalog-model';
import { EntityFilter } from '@backstage/plugin-catalog-react';
export class EnvironmentFilter implements EntityFilter {
  constructor(readonly values: string[]) {}
  filterEntity(entity: Entity): boolean {
    const env = entity.metadata.annotations?.['example.com/environment'];
    return env !== undefined && this.values.includes(env);
  }
}

```
customFil.tsx
```
import { DefaultEntityFilters } from '@backstage/plugin-catalog-react';
import { EnvironmentFilter } from './customfilter';
export type CustomFilters = DefaultEntityFilters & {
  environment?: EnvironmentFilter;
};
```
