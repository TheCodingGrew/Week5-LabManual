# Week5-LabManual

## Select Operation / Querying using LINQ(Language INtegrated Query)
- Language-Integrated Query (LINQ) is the name for a set of technologies based on the integration of query capabilities directly into the C# language
- LINQ looks like SQL
- There are 2 ways to use LINQ - the query syntax and the method syntax. Try them both and choose one which you like the best
```
  LINQ Query Syntax:
  
  var query = from s in db.Songs
            where s.SongAlbum == "Everybody"
            select s;
  foreach(var s in query)
  {
      Console.WriteLine(s.SongName);
  }
  Console.WriteLine(query.Count());
```

```
LINQ Method Syntax:

  var query = db.Songs.Where(s => s.SongAlbum == "Everybody");
  foreach (var s in query)
  {
      Console.WriteLine(s.SongName);
  }
```

- If you are expecting only one result from your query, you can use the First() method
```
  var res = db.Songs.Where(s=>s.SongName=="Bad Blood").First();
  Console.WriteLine(res.SongYear);
```

## Update
- Updating entities can be done by modifying entites directly and saving them to database.
```
  var songResult = from s in db.Songs
                 where s.SongName == "Bad Blood"
                 select s;
  songResult.First().SongYear = 2001;
  db.SaveChanges();
```
The above example is in *query syntax*, but you can modify it to *method syntax* and try the same as well. They are interchangeable and produce the same result.


## Delete
- To delete an entry, query the database and find the entry which you would like removed. Then issue the instruction to delete. Always double check that you only delete rows that must be deleted

```
  var toDelete = db.Songs.Where(s => s.SongName == "En swaasa kaatre").FirstOrDefault();
  db.Songs.Remove(toDelete);
  db.SaveChanges();
```
