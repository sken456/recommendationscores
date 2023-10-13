# recommendationscores
#In this struct, I'm having an issue with the fact that recommendation_scores is a NoneType, So I get problems when it comes to line 24 with the "i" variable --> score = recommendation_scores[i]

def generate_recommendation_scores():
    users = []
    courses = []
    scores = []
    for user_id in test_user_ids:
        test_user_profile = profile_df[profile_df['user'] == user_id]
        # get user vector for the current user id
        test_user_vector = None
        
        # get the unknown course ids for the current user id
        enrolled_courses = test_users_df[test_users_df['user'] == user_id]['item'].to_list()
        unknown_courses = all_courses.difference(enrolled_courses)
        unknown_course_df = course_genres_df[course_genres_df['COURSE_ID'].isin(unknown_courses)]
        unknown_course_ids = unknown_course_df['COURSE_ID'].values
        
        # user np.dot() to get the recommendation scores for each course
        recommendation_scores = None

        # Append the results into the users, courses, and scores list
        for i in range(0, len(unknown_course_ids)):
            score = recommendation_scores[i]
            # Only keep the courses with high recommendation score
            if score >= score_threshold:
                users.append(user_id)
                courses.append(unknown_course_ids[i])
                scores.append(recommendation_scores[i])
                
    return users, courses, scores
