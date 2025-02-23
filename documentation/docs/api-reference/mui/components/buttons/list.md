---
id: list-button
title: List
---

import listButton from '@site/static/img/guides-and-concepts/components/buttons/list/list-mui.png';

`<ListButton>` is using Material UI [`<Button>`](https://ant.design/components/button/) component. It uses the `list` method from [`useNavigation`](/api-reference/core/hooks/navigation/useNavigation.md) under the hood. It can be useful when redirecting the app to the list page route of resource.

## Usage

```tsx title="src/pages/posts/show.tsx"
import { useShow } from "@pankod/refine-core";
// highlight-next-line
import { ListButton, Show, Typography, Stack } from "@pankod/refine-mui";

export const ShowPage: React.FC = () => {
    const { queryResult } = useShow<IPost>();
    const { data, isLoading } = queryResult;
    const record = data?.data;

    return (
        <Show
            isLoading={isLoading}
            cardHeaderProps={{
                action: (
                    // highlight-start
                    <ListButton />
                    // highlight-end
                ),
            }}
        >
            <Stack gap="10px">
                <Typography fontWeight="bold">Id</Typography>
                <Typography>{record?.id}</Typography>
                <Typography fontWeight="bold">Title</Typography>
                <Typography>{record?.title}</Typography>
            </Stack>
        </Show>
    );
};

interface IPost {
    id: number;
    title: string;
}
```

Will look like this:

<div class="img-container">
    <div class="window">
        <div class="control red"></div>
        <div class="control orange"></div>
        <div class="control green"></div>
    </div>
    <img src={listButton} alt="Default list button" />
</div>
<br/>

:::note
The button text is defined automatically by **refine** based on _resource_ object name property.
:::

## Properties

### `resourceNameOrRouteName`

Redirection endpoint(`resourceNameOrRouteName/list`) is defined by `resourceNameOrRouteName` property. By default, `<ListButton>` uses `name` property of the resource object as the endpoint to redirect after clicking.

```tsx
import { ListButton } from "@pankod/refine-mui";

export const MyListComponent = () => {
    return <ListButton resourceNameOrRouteName="categories" />;
};
```

Clicking the button will trigger the `list` method of [`useNavigation`](/api-reference/core/hooks/navigation/useNavigation.md) and then redirect to `/categories`.

### `hideText`

It is used to show and not show the text of the button. When `true`, only the button icon is visible.

```tsx
import { ListButton } from "@pankod/refine-mui";

export const MyListComponent = () => {
    return <ListButton hideText />;
};
```

### `accessControl`

This prop can be used to skip access control check with its `enabled` property or to hide the button when the user does not have the permission to access the resource with `hideIfUnauthorized` property. This is relevant only when an [`accessControlProvider`](/api-reference/core/providers/accessControl-provider.md) is provided to [`<Refine/>`](/api-reference/core/components/refine-config.md)

```tsx
import { ListButton } from "@pankod/refine-mui";

export const MyListComponent = () => {
    return <ListButton accessControl={{ enabled: true, hideIfUnauthorized: true }} />;
};
```

## API Reference

### Properties

<PropsTable module="@pankod/refine-mui/ListButton" />

:::tip External Props
It also accepts all props of Material UI [Button](https://mui.com/material-ui/api/button/).
:::