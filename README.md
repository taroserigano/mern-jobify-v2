
Loaders : are for pre-loading/fetching the data to show on the page  

Actions: are the actions that get triggered when Forms get submitted 

------------------------------------------------------------


QueryClient.ensureQueryData 

is an asynchronous function that retrieves cached data for an existing query. If the query doesn't exist, queryClient.fetchQuery will be called and its results returned. 

The syntax for queryClient.ensureQueryData is: 
const data: = await queryClient.ensureQueryData({ queryKey, queryFn })


-------------------------------------------------------------

const params = Object.fromEntries([
      ...new URL(request.url).searchParams.entries(),
    ]); 

will output the params like {search: 'software', jobstatus'all' .....} 

-------------------------------------------

LOADER : is something that runs when the page loads, 
and returns the value,
which becomes accessible through useLoaderData() like:

  const id = useLoaderData();


--

// for Pre-Loading the data by using userLoadDate() 
export const loader = (queryClient) =>
  async ({ request }) => {
    const params = Object.fromEntries([
      ...new URL(request.url).searchParams.entries(),
    ]);

// you can cache the data like this: 
    await queryClient.ensureQueryData(allJobsQuery(params));
    return { searchValues: { ...params } };
  };

----------

get cache like this: 
const { data } = useQuery(allJobsQuery(searchValues)); 

--------------

The QueryClient is the core of React
 Query. It is responsible for managing the cache, fetching data, and updating the state of your application. 

-it manages the cache 
-it fetches the data 
-it updates the state 

setQueryData: This method sets the data for a specific query.
invalidateQueries: This method invalidates a specific query or all queries.
refetchQueries: This method refetches a specific query or all queries.
-------------------------------------

-staleTime: how soon it refetches the data 

const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      staleTime: 1000 * 60 * 5,
    },
  },
});

-------------------------
REFRESH CACHE: 

The queryClient.invalidateQueries() automatically refetch queries. 

specify or 

queryClient.invalidateQueries(['jobs']);

dont specify, apply for ALL 

queryClient.invalidateQueries();

------------------------------------

  // basicaly, error checking 
  customFetch.interceptors.response.use(
    // check no error ? 
    (response) => {
      // if no, just return as is 
      return response;
    },
    // error found! 
    (error) => {
      if (error?.response?.status === 401) {
        setIsAuthError(true);
      }
      return Promise.reject(error);
    }
  );

---------------------------
























