
<?php
/**
 * 由 PhpStorm 创建。
 * 用户：Overbool
 * 日期：2019-03-21
 * 时间：21:49
 */
get_header();
$categories = get_categories(array(
  '父母' => 0，
));

$bookmarks = get_bookmarks('orderby=date');
$输出 = '';
如果（！空（$书签））{
  $output .= '<ul class="link-items">';
  $output .='<span class="link-title">友情链接</span>';
  foreach ($bookmarks as $bookmark) {
    $output .= '<li class="link-item">';
    $output .= "<a href='$bookmark->link_url' title='$bookmark->link_description' target='_blank'>$bookmark->link_name</a>";
    $output .="</li>";
  }

  $output .='</ul>';
}
$cards = cs_get_option('i_colorful_card');
如果（$cards == null）{
  $cards = array();
}
?>

<div class="content">
  <div class="row">
    <?php foreach ($cards as $card): ?>
      <div class="col-xl-3 col-lg-4 col-6">
        <a class="colorful-card" target="_blank"
           href="<?php echo $card['i_colorful_card_href'] ?>"
           style="background: <?php echo $card['i_colorful_card_color'] ?>">
          <i class="icon <?php echo $card['i_colorful_card_icon'] ?>"></i>
          <?php echo $card['i_colorful_card_title'] ?>
        </a>
      </div>
    <?php endforeach; ?>
    <div class="col-12">
      <div class="index-notice">
        <?php get_template_part('template-parts/notice') ?>
      </div>
    </div>

    <?php
    foreach ($categories 作为 $category) {
      set_query_var('category', $category);
      get_template_part('模板部件/导航卡');
      $terms = wpie_get_child_categories($category->term_id);
      如果（！空（$terms））{
        foreach ($terms as $term) {
          set_query_var('category', $term);
          get_template_part('模板部件/导航卡');
        }
      }
    }
    ?>

    <?php if (cs_get_option('i_link_switcher')): ?>
      <div class="col-12">
        <?php echo $output; ?>
      </div>
    <?php endif; ?>
    <?php if (cs_get_option('i_ad_footer_switcher') && cs_get_option('i_ad_footer_group')): ?>
      <?php foreach (cs_get_option('i_ad_footer_group') as $ad): ?>
        <div class="col-lg-6 bad-footer">
          <?php echo $ad['i_ad_footer_code']; ?>
        </div>
      <?php endforeach; ?>
    <?php endif; ?>

  </div>
  <?php get_footer(); ?>
</div>
