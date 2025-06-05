create a new file in packages/app/src/components/catalog
customentitypage.tsx
```
import {
  Content,
  Header,
  Page,
  ContentHeader,
  SupportButton,
} from '@backstage/core-components';
import { CatalogTable } from '@backstage/plugin-catalog';
import { EntityListProvider, CatalogFilterLayout } from '@backstage/plugin-catalog-react';
const CustomCatalogPage = () => (
  <Page themeId="home">
    <Header title="My Custom Catalog" subtitle="All the components in our org" />
    <Content>
      <ContentHeader title="Components Table">
        <SupportButton>All components registered in the Software Catalog.</SupportButton>
      </ContentHeader>
      <EntityListProvider>
        <CatalogFilterLayout>
          <CatalogFilterLayout.Content>
            <CatalogTable />
          </CatalogFilterLayout.Content>
        </CatalogFilterLayout>
      </EntityListProvider>
    </Content>
  </Page>
);
export default CustomCatalogPage;
```
edit this file 
packages/app/src/app.tsx
```
//add anywherein the import section of the file 
import CustomCatalogPage  from './components/catalog/customentitypage';
//in the flatroute 
<flatroute>
  <Route path="/catalog" element={<CustomCatalogPage />} />

```
adding tabbed view
```
import {
  Content,
  Header,
  Page,
  ContentHeader,
  SupportButton,
} from '@backstage/core-components';
import { Tabs, Tab } from '@material-ui/core';
import { useState } from 'react';
import { CatalogTable } from '@backstage/plugin-catalog';
import { EntityListProvider, CatalogFilterLayout } from '@backstage/plugin-catalog-react';
 
const CustomCatalogPage = () => {
    const [tabIndex, setTabIndex] = useState(0);
  return(
    <Page themeId="home">
    <Header title="My Custom Catalog" subtitle="All the components in our org" />
        <Tabs value={tabIndex} onChange={(_, val) => setTabIndex(val)}>
        <Tab label="Components" />
        <Tab label="APIs" />
      </Tabs>
    <Content>
      <ContentHeader title={tabIndex === 0 ? 'Components' : 'APIs'}>
        <SupportButton>All components registered in the Software Catalog.</SupportButton>
      </ContentHeader>
      <EntityListProvider>
        <CatalogFilterLayout>
          <CatalogFilterLayout.Content>
            <CatalogTable />
          </CatalogFilterLayout.Content>
        </CatalogFilterLayout>
      </EntityListProvider>
    </Content>
  </Page>
  );
  
}
 
export default CustomCatalogPage;
```
customizing column names
```

import {
  Content,
  ContentHeader,
  Header,
  Page,
  SupportButton,
} from '@backstage/core-components';
import {
  
  EntityListProvider,
  CatalogFilterLayout,
  EntityTable,
  useEntityList,
  EntityLifecyclePicker,
} from '@backstage/plugin-catalog-react';
import { EnvironmentPicker } from '../filters/custompicker';
import { BrandedButton } from '../buttons/index.tsx';

const CustomCatalogTable = () => {
  const { entities } = useEntityList();
  const columns = [
    {
      title: 'Name',
      field: 'metadata.name',
    },
    {
      title: 'Type',
      field: 'spec.type',
    },
    {
      title: 'Owner',
      field: 'spec.owner',
    },
    {
      title: 'Lifecycle',
      field: 'spec.lifecycle',
    },
  ];
  return (
    <EntityTable
      title="custom components"
      entities={entities}
      columns={columns}
      emptyContent="No components found."
    />
  );
};
const EntityCatalogPage = () => {
  return (
    <Page themeId="home">
      <Header title="Custom Catalog" subtitle="Enhanced catalog view" />
      <Content>
        <ContentHeader title="Custom Catalog Table">
          <SupportButton>Customized view with new columns and filters</SupportButton>
          <BrandedButton label="Launch Docs" onClick={() => window.open('/docs')} />
          <BrandedButton label="Open Catalog" onClick={() => window.open('/catalog')} />
        </ContentHeader>
        <EntityListProvider>
          <CatalogFilterLayout>
            <CatalogFilterLayout.Filters>
                <EntityLifecyclePicker />
                <EnvironmentPicker />
            </CatalogFilterLayout.Filters>
            <CatalogFilterLayout.Content>
              <CustomCatalogTable />
            </CatalogFilterLayout.Content>
          </CatalogFilterLayout>
        </EntityListProvider>
      </Content>
    </Page>
  );
};

export default EntityCatalogPage;

```
