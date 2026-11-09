# Comic Encyclopedia

A web app for searching and browsing fantasy, horror and science fiction comics from the British Library's open comics dataset. Find a title, see its details and cover, save comics to your own list, and flag records that look wrong.

## Features

- Search by title, author, genre, year and more, with sorting and grouping
- Comic detail pages with cover art (Open Library, falling back to Google Books)
- Accounts with Public, Staff and Admin roles
- Saved lists for signed-in users
- Admin dashboard: top searches, most viewed results, flagged records
- Dataset refresh from the British Library download
- Email sending through SendGrid or Mailjet (optional)
- REST API endpoints for comics, covers and email

## Tech stack

- C# / ASP.NET Core 8 MVC
- Entity Framework Core with SQLite
- ASP.NET Core Identity
- xUnit and Moq for tests
- Docker, GitHub Actions for build and test

## Running it

You need the [.NET 8 SDK](https://dotnet.microsoft.com/download).

```bash
dotnet restore
dotnet run --project src/ComicEncyclopedia.Web
```

Then open the URL shown in the terminal. The SQLite database is created on first run.

### Admin and staff accounts

No passwords are stored in the code. To create the admin and staff accounts on first run, set passwords with user secrets:

```bash
cd src/ComicEncyclopedia.Web
dotnet user-secrets init
dotnet user-secrets set "SeedUsers:AdminPassword" "choose-a-strong-password"
dotnet user-secrets set "SeedUsers:StaffPassword" "choose-a-strong-password"
```

Or as environment variables: `SeedUsers__AdminPassword` and `SeedUsers__StaffPassword`. If they aren't set, those accounts are skipped and you can register normally.

### Email (optional)

Add your SendGrid or Mailjet keys the same way, for example `dotnet user-secrets set "SendGrid:ApiKey" "your-key"`. Never put real keys in `appsettings.json`.

## Tests

```bash
dotnet test
```

## Data

Comic data comes from the British Library's comics dataset, published for research use.
