<template>
    <div class ='about-section'>
            <header class="entry-header">
                <h1 class="entry-title">About me</h1>
            </header>
            <div class="about">
                <div class="about-list row justify-center">

                    <div class="about-item col-2">
                        25 years               
                    </div>
                    <div class="about-item">
                    /
                    </div>
                    <div class="about-item col-2">
                        Data Analyst                
                    </div>
                    <div class="about-item">
                    /
                    </div>
                    <div class="about-item col-2">
                        Aspiring Data Scientist                
                    </div>
                </div>
                <div class="about-description">
                    Prolific, full stack web developer with a passion for metrics and beating former "best-yets." Prototyped 25 new product features per year for Flexor, Inc. Decreased rework by 22% and costs by 15%. Consistently receive high user experience scores for all web development projects, including a 55% increase for Flexor, Inc. Passionate about building world class web applications. One of my sites received a 2015 Webby for Best Navigation and Structure.        
                </div>
            </div>
        <div class="profile-social row justify-center">
                <div class='col-2'>
                    <a  href="https://www.linkedin.com" target="_blank"><i class="fab fa-linkedin fa-3x"></i></a>
                </div>
                 <div class='col-2'>
                    <a  href="https://www.github.com/marcomarson" target="_blank"><i class="fab fa-github fa-3x"></i></a>
                </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'PageIndex',
    props: ['manga']
}
</script>
<style lang='scss'>
.about-section{
    padding:15px 25px;
    text-align: center;
    width: auto;
   .about-item{
       color:$secondary;
       font-weight: bold;
   }
   .profile-social{
        text-align: center;
        // margin-top:15px;
        margin: 25px;
        background-color: $secondary;
     
        a {
             padding:10px;
        display: block;
        color: white;
        text-align: center;
        // padding: 16px;
        text-decoration: none;
        }
        a:hover {
            height: auto;
            width: auto;
            background-color: #111111;
        }
   }
}
</style>
