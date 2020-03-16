# react-simple-provider

Create providers to store your app's data in a normalized fashion 

Access data using `[lookup]` and `[ids]` props in your store.

Set data by dispatching `UPDATE_ITEMS` or `UPDATE_ITEM` actions.

## Installation 

```bash
yarn add react-simple-provider
```

## Usage

```javascript

// user-provider.tsx
import { createProvider } from 'react-simple-provider'

interface IUser {
  id: string;
  name: string;
  image: {
    url: string;
  }
}

const {Provider, useContext} = createProvider<IUser>('User')

export {
  Provider as UserProvider,
  useContext as useUserContext,
}

// app.tsx
import {UserProvider, useUserContext} from './user-provider'

function App() {
  return (
    <UserProvider>
      <Users />
    </UserProvider>
  )
}

function Users() {
  const [state, dispatch] = useUserProvider()

  React.useEffect(() => {
    fetch('/users').then(response => {
      dispatch({
        type: 'UPDATE_ITEMS',
        data: response.data.users
      })
    })
  }, [])


  const users = state.ids.map(id => state.lookup[id])

  return ...
}

```
