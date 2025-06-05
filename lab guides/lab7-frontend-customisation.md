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
in the flatroute 
<flatroute>
  <Route path="/catalog" element={<CustomCatalogPage />} />

```
