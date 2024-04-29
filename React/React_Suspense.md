```tsx
import { useQuery } from '@tanstack/react-query';
import { Suspense } from 'react';
import { BeatLoader } from 'react-spinners';

const getFetchData = async ({ delay }: { delay: number }) => {
  await new Promise((resolve) => setTimeout(resolve, delay));
  const data = await fetch('https://jsonplaceholder.typicode.com/posts/1').then(
    (response) => response.json(),
  );
  return data;
};

type ComponentType = {
  delay: number;
};

const SubComponent = ({ delay }: ComponentType) => {
  const { data } = useQuery(
    ['serverData'],
    () => getFetchData({ delay: delay }),
    { suspense: true },
  );
  return <div>{JSON.stringify(data)}</div>;
};

const App = () => {
  return (
    <Suspense fallback={<BeatLoader color="#424242" />}>
      <SubComponent delay={2000} />
    </Suspense>
  );
};

export default App;
```
