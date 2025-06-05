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
