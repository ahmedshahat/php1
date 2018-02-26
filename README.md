<?php
  ob_start();
	session_start();
	$title = "Category";
	include 'init.php';

	$do = isset($_GET['do']) ? $_GET['do'] :'Manage';


	if ($do == 'Manage') {
		echo "ahmed";
// start page add
	}elseif ($do == 'Add') { ?>

		<h1 class="text-center"> Add Category</h1>
			<div class="container">
					<form class="form-horizontal" action="?do=insert" method="POST">
						<!--  start 	Name  -->
							<div class="form-group form-group-lg">
								<label class="col-sm-2 control-label"> 	Name</label>
								<div class="col-sm-10 ">

									<input type="text" name="	name"  class="form-control" autocomplete="off" required="required" >
								</div>

							</div>
							<!--  end 	Name  -->
							<!--  start 	Description  -->
								<div class="form-group form-group-lg">
									<label class="col-sm-2 control-label"> 	Description</label>
									<div class="col-sm-10 ">
										<input type="text" name="	description"
										 class="form-control  "  placeholder="leave blank if you dont want to change" />

									</div>
								</div>
								<!--  end 	Description  -->
								<!--  start Ordering  -->
									<div class="form-group form-group-lg">
										<label class="col-sm-2 control-label"> Ordering</label>
										<div class="col-sm-10 ">
											<input type="text" name="ordering"  class="form-control" >

										</div>
									</div>
									<!--  end Ordering  -->
									<!--  start Visibility  -->
										<div class="form-group form-group-lg">
											<label class="col-sm-2 control-label"> Visibility</label>
											<div >
												<input id="vis-yas" type="radio" name="Visibility" value="0" checked>
												<label for="vis-yas">yas</label>
											</div>

											<div >
												<input id="vis-no" type="radio" name="Visibility" value="1" >
												<label for="vis-no">no</label>
											</div>

										</div>
										<!--  end Visibility  -->
										<!--  start Allow_comment  -->
										<div class="form-group form-group-lg">
											<label class="col-sm-2 control-label"> Allow_comment</label>
											<div >
												<input id="com-yas" type="radio" name="comment" value="0" checked>
												<label for="com-yas">yas</label>
											</div>

											<div >
												<input id="com-no" type="radio" name="comment" value="1" >
												<label for="com-no">no</label>
											</div>
										</div>
											<!--  end Allow_comment  -->

											<!--  start 	Allow_Ads  -->
											<div class="form-group form-group-lg">
												<label class="col-sm-2 control-label"> 	Allow_Ads</label>
												<div >
													<input id="ads-yas" type="radio" name="Ads" value="0" checked>
													<label for="ads-yas">yas</label>
												</div>

												<div >
													<input id="ads-no" type="radio" name="Ads" value="1" >
													<label for="ads-no">no</label>
												</div>
											</div>
												<!--  end 	Allow_Ads  -->
												<!--  start Add Category  -->
													<div class="form-group form-group-lg ">
														<div class="col-sm-offset-2 col-sm-10 ">
															<input type="submit"  value="Add Category " class="btn btn-success " >
														</div>
													</div>
													<!--  end Add Category  -->
					</form>
			</div>
	<?php
	// end page add

	// start  page insert
}elseif ($do == 'insert') {
	if ($_SERVER['REQUEST_METHOD']== 'POST' ) {

		echo "<h1 class='text-center'> Update Members</h1>";
		echo "<div class = 'container'>";


		$name          = $_POST['name'];
		$descr         = $_POST['description'];
		$ordering      = $_POST['ordering'];
		$Visibility    = $_POST['Visibility'];
		$comment       = $_POST['comment'];
		$Ads           = $_POST['Ads'];


				$check = checkItems("Name", "categories", $name);

				if ($check == 1) {
					$themsg =  "Sorry, this user already exists";
					redirectHome($themsg, 'back');

				}

				else {

							$stmt= $con->prepare("INSERT INTO
																		 categories(name , description , ordering , Visibility , comment, Ads)
																		 VALUES(:zname , :zdesc , :zordering , :zVisibility , :zcomment ,:zAds");
							$stmt -> execute(array(

								'zname'       => $name,
								'zdesc'       => $descr,
								'zordering'   => $ordering,
								'zVisibility' => $Visibility,
								'zcomment'    => $comment,
								'zAds'        => $Ads

							));

							$themsg  = "Member added successfully";
							 redirectHome($themsg, 'back');
				}

	}else {
		echo "<div class='container'>";
		$themsg  = "Member added successfully";
		redirectHome($themsg, 'back');
		echo "</div>";

	}
	echo "<div>";

 include 'includes/tamplates/footar.php';
ob_end_flush();
 ?>
