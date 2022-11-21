# Update-a-city-field-in-contact-when-same-field-is-updated-in-Account-Parent-to-child-update-
Update a city field in contact  when same field is updated in Account{Parent to child update }
trigger updateonContact on Account (after update)
{
   set<id> accounids=new set<id>();
   
     for(Account adb : trigger.new)
       {
           if(adb.BillingCity != trigger.oldmap.get(adb.id).BillingCity)
           {
            accounids.add(adb.id)
           }
        }


 list<Account> accounts=[select id,BillingCity,(select id from contacts) from Account where Id IN:accounids];

 list<contact> con11= new list<contact>();


for(Account a:accounts)
{
      for(Contact c:contacts)
      {
      c . MalingCity= a . Billingcity;
      con11.add(c);
      }
}
update cons;
}

