import java.util.*;
public class RecommendationRunner implements Recommender{
    public ArrayList<String> getItemsToRate (){
        ArrayList<String> res = new ArrayList<String>();
        int numToDisplay = 10;
        int minimalRaters = 5;
        ArrayList<String> res1 = MovieDatabase.filterBy(new TrueFilter());
        Random rand = new Random();
        for(int i = 0; i < numToDisplay; i++){
            int r = rand.nextInt(res1.size());
            String title = res1.get(r);
            if (!res.contains(title)) {
                res.add(title);
            }
        }
        return res;
    }
    public void printRecommendationsFor (String webRaterID){
        FourthRatings fr = new FourthRatings();
        ArrayList<Rating> ratings = fr.getSimilarRatings(webRaterID,1,1);
        int length = 10;
        if(ratings.size()<10){
            length = ratings.size();
        }
        if(ratings.size() == 0){
            int index = 0;
            ArrayList<String> res1 = MovieDatabase.filterBy(new TrueFilter());
            Random rand = new Random();
            HashSet <String> titles = new HashSet <String>();
            for(int i =0; i < 10; i++){
                int r = rand.nextInt(res1.size());
                String title = res1.get(r);
                if (ratings.size()!=0 && !titles.contains(title)) {
                    ratings.add(new Rating(title, 5.00));
                    titles.add(title);
                    index++;
                }
                if(index > 10){
                    break;
                }
            }
        }
