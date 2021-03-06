# Contributors page

We have an official accounting of who is on the Angular Team, who are "trusted collaborators" (see team.angular.io/collaborators), and so on.

The contributors.json should be maintained to keep our "org chart" in a single consistent place.

## GDE listings

There are two pages:

https://developers.google.com/experts/all/technology/angular
(Googlers: source at http://google3/googledata/devsite/content/en/experts/all/technology/angular.html)
which is maintained by Dawid Ostrowski based on a spreadsheet
https://docs.google.com/spreadsheets/d/1_Ls2Kle7NxPBIG8f3OEVZ4gJZ8OCTtBxGYwMPb1TUVE/edit#gid=0

and ours: https://angular.io/about?group=GDE which is derived from contributors.json.

Alex Eagle is investigating how to reconcile these two lists.

## Checking the keys

Keys in contributors.json should be GitHub handles. (Most currently are, but not all)
This will allow us to use GitHub as the default source for things like Name, Avatar, etc.

## Processing the data

Install https://stedolan.github.io/jq/ which is amazing.

```sh
for handle in $(jq keys[] --raw-output < aio/content/marketing/contributors.json)
do echo -e "\n$handle\n---------\n"; curl --silent -H "Authorization: token ${TOKEN}" https://api.github.com/users/$handle \
 | jq ".message,.name,.company,.blog,.bio" --raw-output
done
```
