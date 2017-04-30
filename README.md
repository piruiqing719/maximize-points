/* maximize-points from codewar.com
 the problem is that you have two teams, each player has a ceertain integer to indicate its playpower. Both teams have the same amout of players. The player in team1 plays againest the corresponding one from the team2. Player with higher power will win, and you will get one point otherwise 0. As a coach, you should range the order in your team1 so that you can win the maximum point totally.
strategy to win a game in javascripts*/
function maximizePoints(team1, team2){
  var maxScore = 0;
  return getMaxScore(team1,team2,maxScore);
}

function getMaxScore(team1,team2,maxScore){
//base case for recurssion
  if(team1.length === 1 && team2.length === 1){
    if(team1[0] < team2[0])
      return maxScore;
    else
      return maxScore + 1;
  }
  else {
    var candidates = [];  //pool for chosen the idea is to choose the lowest one to beat your opponents
    for(var i = 0; i < team1.length; i++){
      if(team2[0] < team1[i]){
        candidates.push(team1[i]);
      } 
    }
    if(candidates.length === 0){
      team2.shift();
      var pick = Math.min.apply(null,team1);
      console.log(maxScore);
      console.log(pick);
      var index = 0;
      for(var j = 0; j < team1.length; j++){
          if(pick === team1[j]){
            index = j;
            break;
        }  
      }
      team1.splice(index,1);
      return getMaxScore(team1,team2,maxScore);
    }
    else{
      maxScore += 1;
      var pick = Math.min.apply(null,candidates);
      console.log(maxScore);
      console.log(pick);
      var index = 0;
      for(var k = 0; k < team1.length; k++){
          if(pick === team1[k]){
            index = k;
            break;
        }  
      }
    }
    team1.splice(index,1);
    team2.shift();
    return getMaxScore(team1,team2,maxScore);
  }
}
