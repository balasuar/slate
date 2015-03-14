## Load Locations?
```csharp
    public static void InvokeLocationsImport()
    {
        Login();

        if (_authCookies != null)
        {
            _mi.CookieContainer = _authCookies;

            List<Location_2_0_031> locations = new List<Location_2_0_031>();

            Location_2_0_031 location = new Location_2_0_031();
            location.Description = "ZZ Oil";
            location.EffectiveDate = new DateTime(2009, 1, 1);
            location.Address1 = "123 Main St.";
            location.Address2 = "Suite B.";
            location.City = "Green Bay";
            location.Jurisdiction = "WI";
            location.CountryCode = "USA";
            location.PostalCode = "54313";
            location.OutsideCityLimitInd = YesNo.No;

            locations.Add(location);

            LocationImportResultSummary_2_0_031 result =
                _mi.ImportLocations(locations.ToArray(), "Determination Oil Company", 100, 100, 100, true);

            Dumper.Dump("result", result);
        }
    }
```