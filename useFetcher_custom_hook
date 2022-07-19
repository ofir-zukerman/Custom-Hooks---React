import { useState, useEffect, useCallback } from "react";
import axios from "axios";

interface IUseFetcher {
  loading: boolean;
  data: any;
  error: any;
}

export const useFetcher = (url: string): IUseFetcher => {
  const [fetcher, setFetcher] = useState<IUseFetcher>({
    loading: true,
    data: null,
    error: null,
  });

  const fetchDataFunc: () => Promise<void> = useCallback(async () => {
    try {
      const { data } = await axios.get(url); // we can add token if we wants
      if (data) {
        setFetcher({
          loading: false,
          data: data?.result ?? data,
          error: null,
        });
      }
    } catch (err) {
      console.error(err);
      setFetcher({
        loading: false,
        data: null,
        error: err,
      });
    }
  }, [url]);

  useEffect(() => {
    let unmounted = false;
    fetchDataFunc();
    return () => {
      unmounted = true;
    };
  }, []);

  const { data, error, loading } = fetcher;
  return {
    loading,
    data,
    error,
  };
};
